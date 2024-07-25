# codealpha_tasks_02
login and registration form



#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class User {
public:
    string username;
    string password;

    User(string uname, string pwd) : username(uname), password(pwd) {}
};

bool registerUser(const User &user) {
    ofstream userFile;
    userFile.open(user.username + ".txt");
    if (userFile.is_open()) {
        userFile << user.username << endl;
        userFile << user.password << endl;
        userFile.close();
        return true;
    }
    return false;
}

bool loginUser(const string &username, const string &password) {
    ifstream userFile;
    userFile.open(username + ".txt");
    if (userFile.is_open()) {
        string storedUsername, storedPassword;
        getline(userFile, storedUsername);
        getline(userFile, storedPassword);
        userFile.close();

        if (storedUsername == username && storedPassword == password) {
            return true;
        }
    }
    return false;
}

void registration() {
    string username, password;
    cout << "Enter a username: ";
    cin >> username;
    cout << "Enter a password: ";
    cin >> password;

    User newUser(username, password);
    if (registerUser(newUser)) {
        cout << "Registration successful!" << endl;
    } else {
        cout << "Registration failed!" << endl;
    }
}

void login() {
    string username, password;
    cout << "Enter your username: ";
    cin >> username;
    cout << "Enter your password: ";
    cin >> password;

    if (loginUser(username, password)) {
        cout << "Login successful!" << endl;
    } else {
        cout << "Invalid username or password!" << endl;
    }
}

int main() {
    int choice;

    while (true) {
        cout << "1. Register\n2. Login\n3. Exit\nChoose an option: ";
        cin >> choice;

        switch (choice) {
            case 1:
                registration();
                break;
            case 2:
                login();
                break;
            case 3:
                return 0;
            default:
                cout << "Invalid choice, please try again." << endl;
        }
    }
    return 0;
}
