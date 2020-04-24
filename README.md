# Student-Record-Management-C++
#include <iostream>
#include <conio.h>
#include <fstream>
#include <string.h>
#include <windows.h>
using namespace std;

class OTHERS {
public:
    void newAccount();
    void delAccount();
    void update();
    void search_acc();
    void showAll();
    void Exit();
    void options();
};

void OTHERS::newAccount() {
    //--------------------------------STARTS--------------------------------
    string name, c_name;
    int age = 0;
    char another;

    cout << "\nEnter the following fields:";
    cout << "\n\tName: ";
    cin.ignore();
    getline(cin, name);

    Sleep(200);

    cout << "\n\tAge: ";
    cin >> age;

    Sleep(200);

    cout << "\n\tCourse Name: ";
    cin.ignore();
    getline(cin, c_name);

    ofstream outf;
    outf.open("STUDENTS", ofstream::app);
    outf << name   << "                                   ";
    outf << age    << "                                   ";
    outf << c_name << "                                   " << "\n";
    outf.close();

    cout << "\nAdd another account? (Y/N)";
    cin >> another;
    if (another == 'Y' || another == 'y')
    {
        newAccount();
    }
    else
    {
        system("CLS");
        Sleep(400);
        options();
    }
    //--------------------------------ENDS--------------------------------
}

void OTHERS::delAccount() {
    //--------------------------------STARTS--------------------------------
    fstream Myfile;
    fstream temp;
    string del_name, line;

    cout << "\nEnter student name to delete account: ";
    cin.ignore();
    getline(cin, del_name);

    Myfile.open("STUDENTS", ios::in);
    temp.open("temporary", ios::out);

    while(getline(Myfile, line))
    {
        if(line.find(del_name) != string::npos){}
        else{temp << line << "\n" ;}
    }

    Myfile.close();
    temp.close();
    remove("STUDENTS");
    rename("temporary", "STUDENTS");
    cout << "\n\t\t" << del_name <<"'s " << "Account Successfully Deleted! \n";

    cout << "\nDelete another account? (Y/N)";
    char another;
    cin >> another;
    if (another == 'Y' || another == 'y')
    {
        delAccount();
    }
    else
    {
        system("CLS");
        Sleep(400);
        options();
    }
    //--------------------------------ENDS--------------------------------
}

void OTHERS::update() {
    //--------------------------------STARTS--------------------------------
    fstream Myfile;
    fstream temp1;
    string up_name, line;
    string edit_name = "",  edit_c_name = "";
    int edit_age;

    cout << "\nEnter student name to update account: ";
    cin.ignore();
    getline(cin, up_name);

    Myfile.open("STUDENTS", ios::in);
    temp1.open("temporary1", ios::out);

    while(getline(Myfile, line))
    {
        if(line.find(up_name) != string::npos)
        {
            cout << "Enter Student Name: ";
            //cin.ignore();
            getline(cin, edit_name);

            cout << "Enter Student Age: ";
            cin >> edit_age;

            cout << "Enter Course Name: ";
            cin.ignore();
            getline(cin, edit_c_name);

            temp1 << edit_name <<"                                    ";
            temp1 << edit_age <<"                                   ";
            temp1 << edit_c_name <<"                                   "<< "\n";
        }
        else{temp1 << line << "\n" ;}
    }

    Myfile.close();
    temp1.close();
    remove("STUDENTS");
    rename("temporary1", "STUDENTS");
    cout << "\n\t\t" << up_name <<"'s " << "Account Successfully Updated! \n";

    cout << "\nAny other account to update? (Y/N)";
    char another;
    cin >> another;
    if (another == 'Y' || another == 'y')
    {
        update();
    }
    else
    {
        system("CLS");
        Sleep(400);
        options();
    }
    //--------------------------------ENDS--------------------------------
}

void OTHERS::search_acc() {
    //--------------------------------STARTS--------------------------------
    string srch;
    string line;
    int a;

    ifstream Myfile;
    Myfile.open("STUDENTS");
    cout << "\nEnter Student Name: ";
    cin.ignore();
    getline(cin, srch);

    while(getline(Myfile, line))
    {
        if (line.find(srch) != string::npos)
        {
            cout << "\nSearch Result:" << "\nName:                                   Age:                                   Course:\n" << line << endl;
            a = 1;
        }
    }
    if (a != 1)
    {
        cout << "\nRecord not found!";
    }

    Myfile.close();

    cout << "\nSearch for another record? (Y/N)";
    char another;
    cin >> another;
    if (another == 'Y' || another == 'y')
    {
        search_acc();
    }
    else
    {
        system("CLS");
        Sleep(400);
        options();
    }
    //--------------------------------ENDS--------------------------------
}


void OTHERS::showAll() {
    //--------------------------------STARTS--------------------------------
    string srch;
    string line;

    ifstream Myfile;
    Myfile.open("STUDENTS");
    cout << "\n\t\t\t\tFollowing are all student records: \n\n";

    while(getline(Myfile, line))
    {
        cout << line << "\n";
    }

    Myfile.close();
    Sleep(400);
    char reply;
    cout << "\n\n\n\nReturn to Home? (Y/N)";
    cin >> reply;
    if((reply == 'Y') | (reply == 'y'))
    {
        system("CLS");
        Sleep(400);
        options();
    }
    //--------------------------------ENDS--------------------------------
}

void OTHERS::Exit() {
    exit(0);
}

void OTHERS::options() {
    int opt;
    cout << "\n\nChoose one option: ";
    cout << "\n1. Create New Account \n2. Delete Account \n3. Update Account \n4. Search Account \n5. All records \n6. Exit";
    cout << "\n\n->  ";
    cin >> opt;

    switch (opt)
    {
        case 1:
            Sleep(400);
            system("CLS");
            newAccount();
            break;
        case 2:
            Sleep(400);
            system("CLS");
            delAccount();
            break;
        case 3:
            Sleep(400);
            system("CLS");
            update();
            break;
        case 4:
            Sleep(400);
            system("CLS");
            search_acc();
            break;
        case 5:
            Sleep(400);
            system("CLS");
            showAll();
            break;
        case 6:
            Sleep(400);
            system("CLS");
            Exit();
            break;
        default:
            Sleep(300);
            system("CLS");
            cout << "\n\t\t\t\tChoose a valid option! Try again...";
            Sleep(400);
            options();
            break;
        }
}


//--------------------------------MAIN FUNCTION--------------------------------

int main() {
    OTHERS o;
    string username = "";
    string password = "";
    bool loginSuccess = false;

    cout << "\n\t\t\t\t\tWelcome! Enter Login Details below";
    do{
        cout << "\n\n\t\tUsername:  ";
        cin >> username;
        cout << "\n\t\tPassword:  ";
        cin >> password;

        if(username == "admin" && password == "pass")
        {
            //clear console!!!!!!!!!!!!!!!!!
            cout << "\n\t\t\tLogin Successful!";
            cout << "\n\n";
            Sleep(500);
            system("CLS");
            o.options();
            loginSuccess = true;
        }
        else
        {
            cout << "\n\n\t\tIncorrect username and password combination! Please try again...";
        }
    }while(!loginSuccess);

    return 0;
}
