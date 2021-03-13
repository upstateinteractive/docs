# Apple Account Setup

## Table of Contents
1. [Developer Account](#developer-account)
2. [Set Up Devices Manually](#set-up-devices-manually) 
3. [Set Up Devices via Fastlane](#set-up-devices-via-fastlane) 

## Developer Account
  1. **Free Apple ID**
    An app can be tested on emulators or real devices through XCode with a free personal Apple ID, however, collaborating with a team is difficult since a unique bundle ID is required for the project.
  2. **Apple Developer Program**
    $99/year for development team to work on project together and distribute the app to App Store Connect for Test Flight and the App Store
  3. **Apple Enterprise Program**
    Requires application and $299/year for enterprises with specific use cases that require private distribution directly to employees through a secure internal system
 
Some discussion with your client may be necessary, however, the Apple Developer Program makes sense for the majority of cases. Since you have to pay annually, create the account once the team needs to build the app for testing. 
 
## Set Up Devices Manually

There are specific requirements for developers who are either developing the app on their mac and trying to run it on an iOS device, or distributing the app from their mac to App Store Connect. 

  **1. Certificate Signing Request**
  - The developer has to first make a certificate request from a signing authority in their Keychain Access. 
    - In the Keychain Access menu, go to Keychain Access > Certificate Assistance > Request a certificate from a certificate Authority
    - Enter the email for the Apple ID being used for development
    - Save it to your local disk 

  **2. Certificates**

  - **Development Certificate**: Each developer building iOS on a Mac needs to create a developer certificate.
    - Login to your Apple Developer Account and navigate to “Certificates Identifiers and Profiles”
    - Select App Development
    - Upload the .csr file that you saved. A certificate will be generated for you to download. There will be a public key and a private key created for each device (the private one is kept in the Mac Keychain) the public one is in the Apple Developer Account.
    - It is not necessary to remove/revoke those unless they expire or a developer is no longer tied to the account. 
  
  - **Production/distribution certificate**: These are similar to developer certificates, however they are used in order to distribute your app to iTunes Connect. It is only necessary for the developer distributing the app to create a distribution certificate.
    - Login to your Apple Developer Account and navigate to “Certificates Identifiers and Profiles”. Then select App Distribution. Upload the .csr file that you saved. A certificate will be generated for you to download. There will be a public key and a private key created for each device (the private one is kept in the Mac Keychain) the public one is in the Apple Developer Account. 
    - You do not need to revoke a production certificate unless it expires / or you have generated a new one and updated your provisioning profile. If you revoke one that is tied to the distribution provisioning profile, you'll need to update it.

**3. Identifiers**: A unique identifier needs to be registered for the app in the Apple Developer Account
  - Login to your account
  - Navigate to “Certificates, Identifiers & Profiles” then select App IDs
  - Register the New Identifier by giving it a Bundle ID. It is recommended to use a reverse-domain name style string (com.domainname.appname)  

**4. Provisioning Profiles**
  - **Development Provisioning Profile**: needed in order to test/run the app on a device. It ties the dev certificate, apple ID and device together. We use this in xcode when we test running the app. (ex. it uses your apple id to create a team name, plus the dev certificate generated, plus the device you're running). You can have xcode automatically generate a provisioning profile for you, so you don't have to generate it through your Apple developer account.

  - **Distribution provisioning profile**: needed for App Store submission. It ties the distribution certificate, apple ID and device together. This can be generated automatically through xcode or in your Apple developer account. 
 
### Set Up Devices via Fastlane 
  **1. Install Fastlane**
  [Fastlane Documentation](https://docs.fastlane.tools/)
  [NativeScript Blog](https://www.nativescript.org/blog/automatic-nativescript-app-deployments-with-fastlane#comments)
    
  - NativeScript documentation uses `brew cask install fastlane` approach. If you have trouble getting this to download a new version of fastlane, you can use a Ruby gem approach as follows:
  - Install with ruby version manager
   ```bash
   brew install cruby ruby-install
   ```
   - Add two lines to bottom of ~/.zshrc…
  ```bash
    source /usr/local/opt/chruby/share/chruby/chruby.sh
    source /usr/local/opt/chruby/share/chruby/auto.sh
  ```
   - Open new terminal and add the follow commands:
  ```bash
    ruby --version # (should now be updated to something like 2.6 -- as of 1/8/20)
    gem install fastlane
    fastlane --version # (should show something like 2.137 -- as of 1/8/20)
    gem update fastlane
  ```

  **2. Fastfile**
  Follow the instructions in the NativeScript Fastlane documentation to create/edit the Fastlane folder and Fastfile file in the root of you project. The Fastfile is the main fastlane configuration file. This is where lanes (aka tasks) are specified.

  **3. Appfile**
  - Follow the instructions in the NativeScript Fastlane documentation to create and/or edit the Appfile, which stores information about the app like the app_identifier, apple_id and team_id
  - For example, the sis project includes:
  ```Appfile
    app_identifier "us.sis.ems.mobile"
    apple_id "zoe@upstateinteractive.io"
    team_id "97D7853NMJ"
  ```
  - It is advised to create a new, shared Apple Developer Portal account, something like "office@company.com". This will make sharing access across the team much easier.

  **4. .env.default**
  Store secrets in this file like `MATCH_PASSWORD="xxxxxxxxx"` and add the file to `.gitignore`

  **5. iOS Codesigning**
   - Follow the instructions in the NativeScript Fastlane documentation to set up the "match" approach. Match will generate the necessary certificates and provisioning profiles automatically (no need to access Apple Developer Account page), store encrypted versions of the certificates and provisioning profiles in a repository (Git), and make setup for deployments on a new machine or onboarding a new team member easier. 
    - Install Match
    - Configure Matchfile with project and Apple account information
      - The git_url should link to a separate git repository where you want the encrypted certifcates to go
      - For example, the sis project includes:
      ```
        git_url("https://gitlab.com/sec-spec/ems-fastlane.git")

        storage_mode("git")

        type("development") # The default type, can be: appstore, adhoc, enterprise or development

        app_identifier("us.sis.ems.mobile")
        username("zoe@upstateinteractive.io") # Your Apple Developer Portal username

        team_id("97D7853NMJ")
        team_name("Security Industry Specialists, Inc.")
      ```
  - Follow the documentation to generate certificates and provisioning profiles with Match commands `match development` and `match appstore`
  - Configure the `certificates` lane in your `Fastfile`
  For example, the sis project includes:
    ```
    platform :ios do

      desc 'Fetch certificates and provisioning profiles'
      lane :certificates do
        match(type: 'development')
        match(type: 'appstore')
      end
    ```
  - Install certificates
    ```bash
    fastlane ios certificates
    ````

Now that you are set up, learn more about distributing the app to Testflight [here](./distribution.md)
   
