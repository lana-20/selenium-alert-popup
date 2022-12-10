# Selenium Alerts/Popups

__Alerts / Popups__ (JavaScript alerts)


Click on a button element which opens a Alert window. Normally, can't identify/inspect anything in this Alert window. because alert is not a web element. It's a special type of object.

1) Capture text value of Alert
2) Pass some value into the onput box
3) Close Alert window by clicking 'OK' or "Cancel'. I cannot directly perform the _.click()_ action, so I have to use a different type of function.

To interact with the Alert, WebDriver provides the _.switch_to_ command.

Switch to the alert window which is already open:

	alert_window = driver.switch_to.alert

'alert_window' is an object that represents the whole alert window. From the Alert window I want to capture the text displayed:

	alert_window.text

I want to pass some value into the input box. It it were a normal web element, I'd identify it as a web element and use the _.send_keys()_ method. I can use the alert object directly and send the keys:

	alert_window.send_keys("welcome")

Now I want to close the Alert window by using 'OK' or 'Cancel' button.

__.accept()__ command -> close alert by clicking 'OK' button:

	alert_window.accept()

__.dismiss()__ command -> close alert by clicking 'Cancel' button:

	alert_window.dismiss()

I'm accessing these commands from the alert object, not WebDriver 'driver' object.

_Interview Question_: How to handle alerts/pop-ups?

By using _.switch_to.alert()_ command. I access the command through the 'driver' instance. Once I get that alert in a vaiable/object, I am able to access the rest of the commands through the alert object:

	my_alert = driver.switch_to.alert
	my_alert.text
	my_alert.accept()
	my_alert.dismiss()

Can also try chaining the commands as follows:

	driver.switch_to.alert.accept()
	driver.switch_to.alert.dismiss()
	

__Authentication Popup__

Sometimes, when launching my app, I come across an _Authentication Popup_, which asks for a username and password. It doesn't often happen in prod apps, like an e-commerce website. It occurs mostly in a corporate environment where my Authorization details are required before I can access the app. Companies usually introduce come sort of security for their apps and supply my corporate id and password. Only when I work on a company-specific project, in a particular corporate environment, I run into these kind of web sites.

AUT: http://the-internet.herokuapp.com/basic_auth

Syntax: http://username:password@test.com

Example: http://admin:admin@the-internet.herokuapp.com/basic_auth


How to handle such an __Authentication Popup__? I need to enter the username and password and click the 'Sign in' or 'Cancel' button. There are 2 input fields and 2 buttons.
Alert is not a web element, I cannot interact with it dorectly, and the _.find_element()_ method doesn't work. The only way to hadle this is to _bypass_ the window by providing username and password. This is called __Injection__.

Normally I send the URL and then get this alert window. But sometimes, when I pass the username and password along with the URL, then I can bypass this alert window and directly access the application.

How to specify/inject the username and password inside the URL? Place it between the Protocol and Domain [Name].

![image](https://user-images.githubusercontent.com/70295997/206785270-9413cc79-7f8a-4760-aa6b-07262d535dd5.png)

_admin:admin@_ is not the application username and password. It's not for a regular app, like Amazon, with a typical login page. Not a Login Page where I identify the usename, password and login elements. __Authentication Popups__ are not a part of the app. Such a popup appears before the app, since the browser authenticates whether I am the right person or not. It's an additional window imposed on top of my app. A corporate company intentionally introduces this kind of Authentication Popup before letting me access the app. To verify me as a user, the company internally orientationally imposes this particular window.

Even the _.send_keys()_ method does not work, because there are 2 elements. The _.switch_to.alert_ method does not work either. The only way to handle this is to __inject__ the username and password in to the URL. That bypasses the Authentication Popup.


Bypass the Alert window, go directly to the app Home Page, and verify the Signin Confirmation Message:

	driver.get("https://admin:admin@the-internet.herokuapp.com/basic-auth")

As soon as I enter the [injected] URL, I land on the Home Page (or signin confirmation page).

_Interview Question_: How to handle Authentication Popups/Windows?

I inject my username and password into the URL and then bypass it.

__Notification Popup__

__Notification Popup__ is another type of an Alert Window. I do not see it in every type of app, only in some web apps.

Go to https://whatmylocation.com/.

<img src="https://user-images.githubusercontent.com/70295997/206869783-f92eb571-eebc-485a-a0a7-3a9c548df884.png" width=600></img>

