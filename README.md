<h1>End of Module Assignment<h1/>

<h2>Introduction<h2/>

<h4>Built according to Unit 9's recommendations, this project employs a Python-based security solution for a local grocery store's Online Shopping System (OSS). The basic security issue resolved here is user authentication and access control, noted as a potential OSS vulnerability due to hazards including spoofing, unlawful data access, and privilege escalation.

This solution develops a scalable and safe system for managing users in many roles: customers, managers, and administrators using Object-Oriented Programming (OOP) concepts. The system ensures that every role only use permitted skills, therefore improving the integrity and secrecy of the OSS.<h4/>


Describe of the solution:

2. Explanation of the Solution
Built in Python, this solution shows the safe management of user credentials together with the application of Role-Based Access Control (RBAC). Essential components consist:

Three subclasses—Customer, Manager, and Admin—along with a basic User class form the software. This offers role-specific capability and shows OOP inheritance.

Password security using bcrypt is a strong cryptographic hash method used in the bcrypt library. Hashing guards against data breaches by keeping passwords from being kept in plaintext un encrypted.

Every user role can only act in line with their privileges:

Customers can peruse products.

Managers can change the inventory.

Administrators can handle user accounts.

Registered users are kept in a dictionary simulating a user database. Simplified as it is, this can be developed into a database system for production use.

Passwords entered during login are matched against hashed values using bcrypt.checkpw(), therefore guaranteeing strong and safe authentication.

Strengths of this answer:

shows fundamental OOP ideas in the framework of security.

There is never unencrypted storage for passwords.

Scalable role structure.

Simple for including into more complex systems.

helps reduce STRIDE hazards (such as Spoofing, Elevation of Privilege).

Strengths:

Does not have consistent data storage—no real database.

Ignores account lockout systems or session handling.

Only CLI-based; not yet web or GUI.

Though basic, this solution shows sound programming techniques and basic cybersecurity protections and provides a safe basis to grow on.


3. Instructions to Execute
Prerequisites
•	Python 3.9+ installed
•	bcrypt library installed
To install bcrypt, run:
bash
CopyEdit
pip install bcrypt
To Run the Program
1.	Open your terminal 
2.	Navigate to the directory containing the user_system.py file.
3.	Run the Python file using:
bash
CopyEdit
python user_system.py
 Output
Upon execution, you’ll see:
•	Users being registered with different roles.
•	Login attempts with both valid and invalid credentials.
•	Role-specific actions being executed, such as:
o	browse_items() for customers
o	update_inventory() for managers
o	manage_users() for admins
the code:
import bcrypt

# Base User class
class User:
    def __init__(self, username, password):
        self.username = username
        self.hashed_password = bcrypt.hashpw(password.encode('utf-8'), bcrypt.gensalt())

    def check_password(self, password):
        return bcrypt.checkpw(password.encode('utf-8'), self.hashed_password)

# Subclasses with role-specific actions
class Customer(User):
    def browse_items(self):
        print(f"{self.username} is browsing items.")

class Manager(User):
    def update_inventory(self):
        print(f"{self.username} is updating inventory.")

class Admin(User):
    def manage_users(self):
        print(f"{self.username} is managing user accounts.")

# Simulated user database (in-memory)
user_db = {}

# Function to register a user
def register_user(username, password, role):
    if username in user_db:
        print("Username already exists.")
        return None

    if role == "customer":
        user = Customer(username, password)
    elif role == "manager":
        user = Manager(username, password)
    elif role == "admin":
        user = Admin(username, password)
    else:
        print("Invalid role.")
        return None

    user_db[username] = user
    print(f"{role.capitalize()} '{username}' registered successfully.")
    return user

# Function to log in a user
def login(username, password):
    user = user_db.get(username)
    if user and user.check_password(password):
        print(f"Login successful. Welcome, {username}!")
        return user
    else:
        print("Login failed. Invalid credentials.")
        return None

# ----------------- DEMO ------------------

# Register users
register_user("alice", "password123", "customer")
register_user("bob", "securepass", "manager")
register_user("carol", "adminpass", "admin")

print("\n--- LOGIN ATTEMPTS ---")

# Successful login
user1 = login("alice", "password123")
if isinstance(user1, Customer):
    user1.browse_items()

# Incorrect password
user2 = login("bob", "wrongpass")

# Manager login and action
user3 = login("bob", "securepass")
if isinstance(user3, Manager):
    user3.update_inventory()

# Admin login and action
user4 = login("carol", "adminpass")
if isinstance(user4, Admin):
    user4.manage_users()


The outcome: 
Customer 'alice' registered successfully.
Manager 'bob' registered successfully.
Admin 'carol' registered successfully.

--- LOGIN ATTEMPTS ---
Login successful. Welcome, alice!
alice is browsing items.
Login failed. Invalid credentials.
Login successful. Welcome, bob!
bob is updating inventory.
Login successful. Welcome, carol!
carol is managing user accounts.
Login attempts:
•	 alice (Customer) logged in and could browse items.
•	bob had a failed login attempt with the wrong password (as expected).
•	bob then logged in successfully and could update inventory.
•	carol (Admin) logged in and managed user accounts.



<h2>Conclusion<h2/>
<h4>This Python application demonstrates how well OOP design can be implemented to lower real cybersecurity risks in internet networks. It addresses critical STRIDE issues since it guarantees users are vetted and allowed depending on their responsibilities. By means of password hash, role-based access, and contained class structures, this approach enhances OSS security and offers a practical building block for more demanding systems.

Including a database (e.g., SQLite), GUI/web interface, MFA support, and session management for even more strong security could help next generations of the system. Still, it achieves its primary goal: offer a Python OOP-based, maintainable, expandable, secure, authentication system.<h4/>
