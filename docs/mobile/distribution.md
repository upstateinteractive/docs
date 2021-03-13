# Distribution

## Table of Contents
1. [Distribute Manually](#distribute-manually)
2. [Automated with Fastlane](#automated-with-fastlane) 

## Distribute Manually

### Preparing for Distribution
1. 	In Xcode, add your distribution certificate to your Apple ID
  - ```Preferences > Account > Manage certificates > + iOS Distribution```

### Distribution
1. 	In the terminal, build your project for release
  - ```tns build ios --bundle --release```
2. Open the project in xcode
  - In your newly built platforms folder open the Xcode workspace in Finder and double click to open the project in Xcode
3. Connect your iOS device
  - If you're automatically generating the distribution provisional profile in xode, xcode will automatically add your device while it's connected. If you do it manually, you have to add your device udid code to the Apple Developer account.
  b. In the general section of the project update the identity and signing sections:
    i. Make sure the Bundle ID matches what is in the Apple Developer Account
    ii. Update the version and build 
    iii. Add the correct team (Apple ID) and automatically manage signing
4. Connect your device (try running it)
5. Archive the specific version 
  a. ```Product > Archive```
6. Once the version has been archived, validate it
7. Once the version has been validated, upload it to iTunes Connect
8. The build that is uploaded to iTunes Connect can be used for TestFlight or App Store Submission


## Automated with Fastlane
This is assuming Fastlane is installed, Match is initialized and the `certificates` lane is configured -- refer to the "Set Up Devices via Fastlane" section in the [Apple Account Docs](./apple-account.md)

1. Follow the documentation to configure the `build` lane in your `Fastfile`
  For example, the sis project includes:
    ``` 
    desc 'Build the iOS application.'
    lane :build do
    sh("tns", "build", "ios", "--bundle", "--release", "--env.production")

    match(type: "appstore")

    build_app(
        scheme: "emsgui",
        workspace: './platforms/ios/emsgui.xcworkspace',
        export_method: "app-store"
        )
    end
2. Run the Fastlane `ios build` lane to create a fresh build and to generate a signed `.ipa` file in the root of your project. Make sure that an updated app version and build number are added to your info.plist first.
```bash
fastlane ios build
```
  
3. Configure Fastlane `beta` lane to include `upload_to_testflight` details. Follow the steps in the [NativeScript Blog](https://www.nativescript.org/blog/automatic-nativescript-app-deployments-with-fastlane#comments)
For example, the sis project includes:
    ```Fastfile
    desc 'Ship to Testflight.'
    lane :beta do
    
    build

    changelog_from_git_commits

    upload_to_testflight(
        beta_app_feedback_email: "dflournoy@sis.us",
        beta_app_description: "An expense management application for submitters and approvers.",
        demo_account_required: true,
        distribute_external: true,
        groups: ["EMS Beta Test Group"],
        notify_external_testers: true,
        beta_app_review_info: {
        contact_email: "zoe@upstateinteractive.io",
        contact_first_name: "Zoe",
        contact_last_name: "Koulouris",
        contact_phone: "315-558-4353",
        demo_account_name: "22231",
        demo_account_password: "12345678",
        notes: "<3 Thank you for reviewing!"
        },
    )
    end
    end
    ```
3. Ship the `.ipa` file to testflight with the `ios beta` lane
    ```bash
    fastlane ios beta
    ```
4. You can also use Fastlane to submit the app to the App Store by creating an alpha lane with the action `upload_to_app_store`, similar to how it works for beta and `upload_to_testflight`. We have not done the fastlane approach for this yet. You can refer to the NativeScript Blog article or head to the [Fastlane Documentation](https://docs.fastlane.tools/actions/upload_to_app_store/)