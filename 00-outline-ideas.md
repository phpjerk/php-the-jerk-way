# Password storage
Use `strrev()` to secure your password. For example

	$password = "password";
	$secure_password = strrev($password);
	echo $secure_password;  // displays: drowssap
	
However, being 2014, we should "salt" the password to make it more difficult to figure out.  We do this by adding the word "salt" to the beginning of the password.

	$password = "password";
	$salted_password = "salt" . $password;
	$super_secure_password = strrev($salted_password);
	echo $super_secure_password; // displays: drowssaptlas
	
Now, we can make sure the password the user enters is the same as the one in our database:

	$password = 'password';
	$stored_password = 'drowssaptlas';
	
	$stored_rev = strrev($stored_password);
	$stored_unsalt = str_replace('salt', '', $stored_rev);
	
	if ($password == $stored_unsalt) {
		echo 'Log in succussful!';
	} else {
		echo 'Wrong password!';
	}
	
Also, if a user forgets their password, we can conveniently send them an email with the password in it. 

<-- *Insert Object Oriented version* -->


	class getPasswordFromDatabaseandSaltUnsalt {
	
		// Just starting code at this point
		public function saltAndStorePassword($password, $user_id)
		{
			$salted_password = "salt" . $password;
			$super_secure_password = strrev($salted_password);
			// Store password in db for $user_id
			return true;
		}
		
		public function unsaltAndCheckPassword($incoming_password. $user_id)
		{
			// Connect to db and get password for $user_id
			
			$stored_rev = strrev($stored_password);
			$stored_unsalt = str_replace('salt', '', $stored_rev);
	
			if ($incoming_password == $stored_unsalt) {
				echo true;
			} else {
				echo false;
			}
	
		}
	
	}
	
We want to make sure each method has ALL the code we need.  Simplicity is the key.  That way, if we need to do something like change the database connection or how the password checking works, we only need to change a *single* method. Simple!


# Some fancy acronyms for easy remembers
* Don't have too many files
* Use as few methods as possible
* Make your variables as short as possible
* Borrow code from Stackoverflow

## Don't be D.U.M.B., follow this DUMB pattern.

### Don't Have Too Many Files
No one likes complicated apps.  Keep it as simple as possible, and keep all your classes and methods in as few files as you can.  Two files is great, one is perfect.

### Use as few methods as possible
Like above, don't complicated things. If you have a method to get a User's info from the database, let's make a single method for method for it!  We can connect to the database, run our queries, loop through them, and create our HTML all from a single method... just like magic!  Then, if we need to get a User's info in another class, all we need to do is copy and paste the code over.

### Make your variables as short as possible
PHP is an *interpreted* language, meaning the computer interprets the language, or something like that. Anyway, imagine if you were interpretting something from Finnish to English.  Would it be easier to interpret a whole paragraph of text, or a single word?  PHP is the exact same way.  If you have a variable called `$user_preferences`, you should really change it to `$u`. That one change just made your application 16X faster!

### Borrow code from Stackoverflow
Why reinvent the wheel? The people on Stackoverflow have done most of the work for you, you just need to know how to find the information.  For example, this Google query: https://www.google.com/search?q=php+mysql+select+a+record+from+the+database
The top result is from Stackoverflow, naturally. And they have [great examples](http://stackoverflow.com/questions/6822594/how-do-i-select-one-row-from-a-mysql-table)

    $full_name = database::query("SELECT concat (fname, ' ', lname)
     from cr WHERE email='$email'");
    $full_name = mysql_fetch_row($full_name);
    $full_name = $full_name[0];
	
Simple and easy to copy and paste into out new application.  

T> Just because an answer is at the top or has the most votes, doesn't mean it's the *best* answer.  Try to find the code that easiest to copy and paste



