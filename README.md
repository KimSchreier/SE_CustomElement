SE_CustomElement
================

This Repo is for everyone that wants to take part in creating a custom Polymer element.

***

# Guide

## 1. Setup

#### 1.1 clone this [Reposetory](https://github.com/KimSchreier/SE_CustomElement.git)


#### 1.2 make a bower update

> $ bower update 

therefor you will need [bower](http://bower.io/) and [nodejs](http://nodejs.org/), 

or get the Polymer elements by your self [**here**](https://www.polymer-project.org/docs/start/getting-the-code.html) and the webcomponentjs [**here**](https://github.com/webcomponents/webcomponentsjs)

#### 1.3 Code editor

I will use [Brackets](http://brackets.io/). But you can take what you want to edit html code.

## 2. Coding

### 2.1 Overview

**/bower_components**
> * Polymer core and paper elemnts
> * webcomponentsjs

**/web**
> * import.html - Summary of all imports that we will need.
> * index.html - main page.
> * contact-contacts.html - main application, handling of view, data binding, ...
> * contact-card.html - template for a contact card


### 2.2 index.html
 
#### Import contact-contacts.html
```html
<link rel="import" href="contact-contacts.html">
```

#### custom tag: contact-contacts
```html
<body>
   <contact-contacts></contact-contacts>
</body>
```

### 2.3 contact-contacts.html



#### Import contact-card.html

```html
<link rel="import" href="contact-card.html">
```


#### Data Binding - Changing Heading 

###### 1. Replace Contacts with {{heading}} 

```html
 <div id="div" tool>Contacts</div>
```
to:

```html
 <div id="div" tool>{{heading}}</div>
```
###### 2. Add a default property for heading
```javascript
ready: function(){
    this.heading = "All Contacts",       
```
###### 3. Set the text for your heading in the functions view_all() and view_favored()
```javascript
            this.view_favored = function (){
                this.$.favored.style.display = 'block';
                this.$.all.style.display = 'none';
                this.heading = "Favorite Contacts";
            },
            this.view_all = function (){
                this.$.favored.style.display = 'none';
                this.$.all.style.display = 'block';
                this.heading = "All Contacts";
            }
```

#### 