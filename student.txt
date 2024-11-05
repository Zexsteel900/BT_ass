// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StudentData {
    
    // Structure to hold student details
    struct Student {
        string fullName;
        uint8 ageInYears;
        string course;
    }
    
    // Array to store student records
    Student[] public students;

    // Event to emit when a new student is added
    event StudentAdded(string fullName, uint8 ageInYears, string course);

    // Fallback function to handle plain Ether transfers
    fallback() external payable {
        // Fallback function can be used to receive funds with data
    }

    // Receive function to handle plain Ether transfers
    receive() external payable {
        // This function will be called when Ether is sent without any data
    }

    // Function to add a student
    function addStudent(string memory _fullName, uint8 _ageInYears, string memory _course) public {
        // Create a new student instance
        Student memory newStudent = Student({
            fullName: _fullName,
            ageInYears: _ageInYears,
            course: _course
        });
        
        // Add the new student to the array
        students.push(newStudent);
        
        // Emit the event
        emit StudentAdded(_fullName, _ageInYears, _course);
    }

    // Function to retrieve student details by index
    function getStudent(uint256 _index) public view returns (string memory fullName, uint8 ageInYears, string memory course) {
        require(_index < students.length, "Student index out of bounds");
        
        // Get the student details from the array
        Student memory student = students[_index];
        return (student.fullName, student.ageInYears, student.course);
    }

    // Function to get the total number of students
    function getStudentCount() public view returns (uint256) {
        return students.length;
    }
}
