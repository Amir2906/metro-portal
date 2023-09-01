# Project : Metro Portal

## Description :

	This project is used to book Metro tickets for Ahmedabad citizens. Using this GUI application user can do signup and login. During signup process I used twilio API to send otp to verify mobile number. Once mobile number is verified user will be added to database. User needs to issue smart card before booking tickets. Once user has issued smart card he/she can book tickets using this portal. User can also check his/her previously booked tickes.

## Packages Required :
	1. tkinter : For Graphical User Interface
	2. mysqlconnector : For Connecting MySQL database
	3. twilio : For OTP service

## Installation :
	1. tkinter : pip install tk
	2. mysqlconnector : pip install mysql-connector-python
	3. twilio : pip install twilio


## Sign-Up & Other setup for Twilio :
	1. You have to do sign-up on their website to use their	API services of SMS sending
	2. copy account_sid,auth_token and phone number which will given by them to code in 'signup.py' file's details, right now my account details are already in code.


## Tables Required :
	1. Username will be by default 'root'
	2. set Password as '' , can be changed it later on.
	3. Execute these below commands One by One to create tables.

	create database passenger;

	use passenger;

	create table login(
		first_name varchar(20),
		last_name varchar(20),
		username varchar(30) primary key,
		password varchar(30),
		confirm_password varchar(30),
		age varchar(5),
		contact varchar(30)
	);

	create table ticket(
 		id int primary key AUTO_INCREMENT,
		username varchar(30),
		pnr int,
		source varchar(20),
		destination varchar(20),
		rate int,
		constraint FK_passengers_username foreign key (username) references login(username)
 	);

	create table card(
		username varchar(30) primary key,
		amount int,
		constraint FK_card_username foreign key (username) references login(username)
	);
	

## Working of Project :
	1.	User can sign-up, using email id, phone number and other details, data will be stored in database and email id/username is primary key, so no duplicate value is allowed of that field
	2.	Real time OTP will be sent on User's Phone number, only by verifying it, User will able to create Account.
	3.	Login window is provided for user, after only Successful Login username and password it'll redirect User to Dashboard.
	4.	On dashboard there are 4 different features,
		a. booking window
		b. Create SmartCard
		c. Recharge SmartCard
		d. View Previous Transaction
	5.	SmartCard balance is essential for booking Metro Ticket
	6.	We have considered, 4 Metro Trains running b/w different stations, but their ending station is same, so user can travel among all the places.
	7.	Fare is calculated upon station distances.
	8.	In booking window, user will get options to select source and destination stations, then it will show Fare and ask user to give username, which will check smart card issued or not, if issued already then it has enough balance or not.
	9.	If it has enough balance then it will charge that amount from database and issue ticket, which will pop up using small window, & data can be retrieved using 'show transaction' option in dashboard.
	10.	User can also add balance in SmartCard.

## Website of Twilio :
	https://www.twilio.com/docs/usage/api

## How to Run :
	python3 app.py