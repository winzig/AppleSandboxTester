# AppleSandboxTester
It can be tedious to create new test users in Apple's iTunes Connect Sandbox, especially when testing In-App Purchase, where you often need a clean test user in the sandbox. Here you'll create a bookmarklet that will help you create test users quickly.

First, drag this bookmark to your bookmarks menu: **[Sandbox Tester](http://replaceme)**

Then right-click on the bookmark and select "Edit Address..." (in Safari, anyway).

Paste this JavaScript in as the new address:

    javascript: 
    var password = 'SandboxSux1';
    var classesToAdd = 'ng-isolate-scope ng-dirty ng-valid hasVisited ng-valid-required'; 
    var classesToRemove = 'ng-pristine ng-invalid ng-invalid-required invalid-srvr';
    var press = jQuery.Event("change");
    $(document.forms[0][0]).val('John').addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][1]).val('Doe').addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][4]).val(prompt('Email?', '')).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][5]).val(password).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][6]).val(password).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][7]).val('Random Number').addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][8]).val(Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10)).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][9]).prop("selectedIndex",1).trigger(press);
    $(document.forms[0][10]).prop("selectedIndex",1).trigger(press);
    $(document.forms[0][11]).prop("selectedIndex",148).trigger(press);
    $( "button, input[type='button']" ).attr('disabled', false).click();

When you're on the [Add Sandbox Tester](https://itunesconnect.apple.com/WebObjects/iTunesConnect.woa/ra/ng/users_roles/sandbox_users/new) page, you can now click the new "Sandbox Tester" bookmark, and it will fill in the form and submit it. Note that you will probably want to edit some of the JavaScript to suit your preferences.

## What It Looks Like

<img src="https://raw.githubusercontent.com/winzig/AppleSandboxTester/master/UsingAppleSandboxTester.gif" width="400" height="360"/>

## What It Does

Using JavaScript, it fills in the following values:

  * First name: `John`
  * Last name: `Doe`
  * Email: Prompts for Email
  * Password: `SandboxSux1` *CHANGE THIS!*
  * Secret Q&A: 15 digit random number
  * Birthday: `January 1`
  * Country: `United States`

Then for each field, it messes with the classes and simulates a "change" event, to fool the form into accepting a submission from you without you physically typing into the fields. 

You can speed things up even more if you have a Gmail account (or any email provider that allows you to create alias addresses by appending "+something" to your username). Use the below bookmarklet, and set your gmail username and domain below near the top of the script before pasting it into the bookmarklet. 

The bookmarklet will then no longer ask you to pick an email address, but will instead fill it in for you as **yourusername**+sandbox*[number]*@**yourdomain.com**. The *[number]* just uses the number of seconds since the epoch. 

    javascript: 
    var password = 'SandboxSux1';
    var gmailuser = 'yourusername';
    var gmaildomain = 'yourdomain.com';
    var classesToAdd = 'ng-isolate-scope ng-dirty ng-valid hasVisited ng-valid-required'; 
    var classesToRemove = 'ng-pristine ng-invalid ng-invalid-required invalid-srvr';
    var press = jQuery.Event("change");
    $(document.forms[0][0]).val('John').addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][1]).val('Doe').addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][4]).val(gmailuser + '+sandbox' + (new Date()).getTime() + '@' + gmaildomain).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][5]).val(password).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][6]).val(password).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][7]).val('Random Number').addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][8]).val(Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10) + '' + Math.floor(Math.random()*10)).addClass(classesToAdd).removeClass(classesToRemove).trigger(press);
    $(document.forms[0][9]).prop("selectedIndex",1).trigger(press);
    $(document.forms[0][10]).prop("selectedIndex",1).trigger(press);
    $(document.forms[0][11]).prop("selectedIndex",148).trigger(press);
    $( "button, input[type='button']" ).attr('disabled', false).click();
    
## Known Issues

  * After the bookmarklet submits the form, clicking the "+" button to create a new user doesn't seem to work. Not sure why yet, but what I do is just create another (regular) bookmark to the [Add Sandbox Tester](https://itunesconnect.apple.com/WebObjects/iTunesConnect.woa/ra/ng/users_roles/sandbox_users/new) page, and use that.

If you spot any other problems, please submit a pull request!
