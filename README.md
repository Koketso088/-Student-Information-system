#include <iostream>
#include <vector>
using namespace std;

class Student {
public:
    string id;
    string name;
    float scores[3];
    float average;
    char grade;

    void inputData() {
        cout << "Enter ID: ";
        cin >> id;
        cout << "Enter Name: ";
        cin.ignore();
        getline(cin, name);

        cout << "Enter 3 test scores: ";
        float sum = 0;
        for (int i = 0; i < 3; i++) {
            cin >> scores[i];
            sum += scores[i];
        }
        average = sum / 3;

        if (average >= 75) grade = 'A';
        else if (average >= 65) grade = 'B';
        else if (average >= 55) grade = 'C';
        else if (average >= 45) grade = 'D';
        else grade = 'F';
    }

    void displayData() {
        cout << id << "\t" << name << "\t" << average << "\t" << grade << endl;
    }
};

int main() {
    vector<Student> students;
    int choice;

    do {
        cout << "\n=== Student Management System ===\n";
        cout << "1. Add Student\n";
        cout << "2. Display All Students\n";
        cout << "3. Search by ID\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        if (choice == 1) {
            Student s;
            s.inputData();
            students.push_back(s);
        }
        else if (choice == 2) {
            cout << "ID\tName\tAverage\tGrade\n";
            for (auto &s : students)
                s.displayData();
        }
        else if (choice == 3) {
            string sid;
            cout << "Enter ID to search: ";
            cin >> sid;
            bool found = false;
            for (auto &s : students) {
                if (s.id == sid) {
                    s.displayData();
                    found = true;
                }
            }
            if (!found) cout << "Student not found!\n";
        }
    } while (choice != 4);

    return 0;
}

