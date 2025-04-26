struct Student {
    string firstName;
    string lastName;
    string studentID;
    int numTests;
    float* testScores;
};


int getNumber() {
    ifstream file("student.dat");
    int count = 0;
    string line;

    while (getline(file, line)) {
        count++;
    }

    file.close();
    return count;
}


void removeStudent(const string& targetID) {
    int numStudents = getNumber();
    if (numStudents == 0) {
        cout << "No student data found." << endl;
        return;
    }

    Student* students = new Student[numStudents];


  
  ifstream inFile("student.dat");
    bool found = false;
    int actualCount = 0;

    for (int i = 0; i < numStudents; ++i) {
        if (!getline(inFile, students[i].firstName, ' '))
            break;
        getline(inFile, students[i].lastName, ' ');
        getline(inFile, students[i].studentID, ' ');

        string numTestsStr;
        getline(inFile, numTestsStr, ' ');
        students[i].numTests = stoi(numTestsStr);

        students[i].testScores = new float[students[i].numTests];

        for (int j = 0; j < students[i].numTests; ++j) {
            string scoreStr;
            if (!(inFile >> scoreStr)) break;
            students[i].testScores[j] = stof(scoreStr);
        }


        inFile.ignore();


        if (students[i].studentID == targetID) {
            found = true;
            continue; // Skip adding this student to final file
        }

        students[actualCount++] = students[i]; // Keep only unmatched
    }

    inFile.close();

    if (found) {
        ofstream outFile("student.dat");
        for (int i = 0; i < actualCount; ++i) {
            outFile << students[i].firstName << " "
                    << students[i].lastName << " "
                    << students[i].studentID << " "
                    << students[i].numTests;

            for (int j = 0; j < students[i].numTests; ++j) {
                outFile << " " << students[i].testScores[j];
            }
            outFile << endl;
        }

        outFile.close();
        cout << "Student with ID " << targetID << " removed successfully." << endl;
    } else {
        cout << "Student with ID " << targetID << " not found." << endl;
    }


