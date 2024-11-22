
# Student Performance Tracker

## Overview

This Python program tracks student performance based on their scores in four subjects: **English**, **Science**, **Math**, and **Urdu**. 
The program allows users to input student names and scores, calculates individual averages, determines pass/fail status, and calculates the class average.

---

## Features

1. **Student Management**
   - Add multiple students with their respective scores.
   - Automatically calculate each student's average score.
   - Determine if a student is passing based on a customizable passing score (default: 35).

2. **Class Performance**
   - Calculate the overall class average based on all students' average scores.
   - Display each student's performance in a formatted output.

3. **Input Handling**
   - Validates that scores are numerical.
   - Ensures student names are not empty.

---

## Code Implementation

### `Students` Class
```python
class Students:
    def __init__(self, name, scores):
        self.name = name
        self.scores = scores

    def calculate_average(self):
        if not self.scores:
            return 0
        return sum(self.scores) / len(self.scores)

    def is_passing(self, passing_score=35):
        return all(score >= passing_score for score in self.scores)
```
### `PerformanceTracker` Class
```python
class PerformanceTracker:
    def __init__(self):
        self.students = {}

    def add_student(self, name, scores):
        self.students[name] = Students(name, scores)

    def calculate_class_average(self):
        if not self.students:
            return 0
        total_scores = sum(student.calculate_average() for student in self.students.values())
        return total_scores / len(self.students)

    def display_student_performance(self):
        for name, student in self.students.items():
            avg = student.calculate_average()
            status = "Passing" if student.is_passing() else "Failing"
            print(f"{name}: Average Score = {avg:.2f}, Status = {status}")
```
### Helper Function: `get_student_data`
```python
def get_student_data():
    while True:
        try:
            name = input("Enter student's name: ").strip()
            if not name:
                print("Name cannot be empty. Try again.")
                continue

            scores = []
            for subject in ["English", "Science", "Math", "Urdu"]:
                score = int(input(f"Enter {name}'s score for {subject}: "))
                scores.append(score)

            return name, scores
        except ValueError:
            print("Invalid input. Please enter numerical scores.")
```
### Main Function
```python
def main():
    tracker = PerformanceTracker()

    print("Welcome to the Student Performance Tracker!")
    while True:
        name, scores = get_student_data()
        tracker.add_student(name, scores)

        more = input("Do you want to add another student? (Yes/No): ").strip().lower()
        if more != "yes":
            break

    print("\nProcessing Results...\n")
    tracker.display_student_performance()
    print(f"Class Average Score: {tracker.calculate_class_average():.2f}")
```
---

## Example Execution

### Input:
```
Welcome to the Student Performance Tracker!
Enter student's name: John Doe
Enter John's score for English: 45
Enter John's score for Science: 50
Enter John's score for Math: 35
Enter John's score for Urdu: 40
Do you want to add another student? (Yes/No): yes
Enter student's name: Jane Smith
Enter Jane's score for English: 30
Enter Jane's score for Science: 25
Enter Jane's score for Math: 40
Enter Jane's score for Urdu: 50
Do you want to add another student? (Yes/No): no
```

### Output:
```
Processing Results...

John Doe: Average Score = 42.50, Status = Passing
Jane Smith: Average Score = 36.25, Status = Failing
Class Average Score: 39.38
```

---

## Enhancements

1. **Data Persistence**
   - Save and load student data from a file to retain information between sessions.

2. **Graphical Output**
   - Use libraries like `matplotlib` to create visualizations for scores and performance distribution.

3. **Validation**
   - Ensure scores are within a valid range (e.g., 0-100).

---

## Conclusion

This program is a simple yet effective way to manage and track student performance. With additional features, it can be extended into a more comprehensive solution for educators.
 n