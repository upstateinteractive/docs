# And ESLint was Good.

## Intro
Substance over style. But don't be unkempt.  
  
[ESlint](http://www.eslint.org) is the tool we use for keeping our JavaScript code clean and standardized.  

A linter will check your JavaScript files for obvious errors like unclosed paratheses. But it will also check for variables that are declared but never used. It will check for any `console.log`s that shouldn't be there.  
  
In total, a linter will check your JavaScript against a set of style and syntax rules and notify you if you've broken one. 

## Installation
### npm  
  
```
npm install --save-dev eslint
```
We only need `eslint` when we are developing. So we save it as a development dependency.  

### alias
you'll be able to call `eslint` from the command line, from the root of your project, by using:
```
node_modules/.bin/eslint <command>
```

However, this is not exactly convenient if you're using `eslint` from the command line frequently. So you should make an alias in your `.aliases` dotfile:
```
alias eslint="node_modules/.bin/eslint"
```

## Usage
### Node
For a node project, AirBnB's style guide is the starting point for our eslint configuration.

```
elsint --init
```
Select **Use a popular style guide** then **Airbnb** then **N** then **JSON**
  
We make a single modification to the rules, we turn off the `no-console` rule. Because in node, console is used a lot to output information to users.  

_**.eslint.json**_
```json
{ 
  "extends": "airbnb-base",
  "plugins": [
    "import"
  ],
  "rules": {
    "no-console": "off"
  }
}
```

### Angular 1x
For angular 1x, we use sensible community supported configurations.

```
npm i -D eslint-config-angular eslint-plugin-angular
```  

_**.eslint.json**_
```json
{
  "extends": "angular"
}
```

## Editor Configuration
### Atom
Installing eslint requires two packages:  

1. **linter** A Base Linter with Cow Powers
2. **linter-eslint** Lint JavaScript on the fly, using ESLint  
  
Both packages can be found easily from the Install pane of Atom's preferences.


### Vim
To use ESlint with Vim you must have [Syntastic](https://github.com/vim-syntastic/syntastic#installation) installed. 
  
#### .vimrc  
Add the following to your `.vimrc` file.  

##### Great Syntastic Settings 
From: [In Editor Linting with Syntastic](https://medium.com/usevim/in-editor-linting-with-syntastic-6814122bdbec#.482x2jyh1) by Alex R. Young  

```
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*
let g:syntastic_always_populate_loc_list = 1
let g:syntastic_loc_list_height = 5
let g:syntastic_auto_loc_list = 0
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 1
let g:syntastic_javascript_checkers = ['eslint']
let g:syntastic_error_symbol = '❌'
let g:syntastic_style_error_symbol = '⁉️'
let g:syntastic_warning_symbol = '⚠️'
let g:syntastic_style_warning_symbol = '💩'
highlight link SyntasticErrorSign SignColumn
highlight link SyntasticWarningSign SignColumn
highlight link SyntasticStyleErrorSign SignColumn
highlight link SyntasticStyleWarningSign SignColumn
```

##### Use Local ESLint
From: [Using Vim with Syntastic and ESLint](http://remarkablemark.org/blog/2016/09/28/vim-syntastic-eslint/) by "Remarkable Mark"  

```
let g:syntastic_javascript_eslint_exe = '$(npm bin)/eslint'
```
