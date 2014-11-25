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

#### Repeat a Template - Add all contact-cards

add the following to the div with the id: "all"
```html
<template repeat="{{contact in contacts}}">
     <contact-card></contact-card>
</template>
```

#### Conditional Template - Add favored contact-cards

add the following to the div with the id: "favored"
```html
 <template repeat="{{contact in contacts}}" >
        <template if="{{contact.favored === 'true'}}">
            </contact-card>
        </template>
</template>
```

### 2.4 contact-card.html

#### The basic Template
```html
        <div id="card">
            <paper-shadow id="shadow">
                <paper-fab icon="" id="paper_icon_button" on-tap="{{favor}}"></paper-fab>
                    <div style="display: flex"><p class="name"> name </p></div> 
                    <p class="phone"> phone-number </p>
                    <div class="group"> group </div>   
            </paper-shadow>
        </div>
```

#### Attributes of the custom tag

```html
    <polymer-element name="contact-card" attributes="name phone group favored icon on-favorite-tap">
```

#### create placeholders for the attributes

by adding this to the Polymer script:

```javascript
        favor: function(event, detail, sender){
            this.asyncFire('favorite-tap');
        },
        name: "name-placeholder",
        phone: "phone number",
        group: "group-placeholder",
        favored: "false",
        icon: "menu"
 ```         

#### Set the attributes by refering to this tag - Data Binding

Now you have to set the attribute values in the contact-contacts.html
```html
                        <contact-card name="{{contact.name}}" 
                                      phone="{{contact.phone}}" 
                                      group="{{contact.group}}" 
                                      favored="{{contact.favored}}"  
                                      icon="{{contact.icon}}"
                                      on-favorite-tap="{{handleFavorite}}">
                        </contact-card>
 ``` 