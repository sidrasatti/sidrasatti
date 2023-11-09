#include<iostream>
#include<string>
using namespace std;
class Course
{
private:
string Course_Name;
string* students;
int No_Of_Students;
int capacity_of_students;
public:
Course( const string& Course_Name, int capacity_of_students);//parameterized constructor
Course( Course& obj);//deepcopy constructor
~Course();//using destructor
string get_Course_Name();
void add_student(const string& name);
void drop_student(const string& name);
string* get_student();//getting array of students
int get_No_Of_Students();
};
//implementing the work of parameterized constructor
Course::Course(const string& Course_Name, int capacity_of_students)
{
No_Of_Students = 0;
this->Course_Name = Course_Name;
this->capacity_of_students = capacity_of_students;
students = new string[capacity_of_students];
}
// Implementing the work of deep copy constructor
Course::Course(Course& obj)
{
Course_Name = obj.Course_Name;
No_Of_Students = obj.No_Of_Students;
capacity_of_students = obj.capacity_of_students;
students = new string[capacity_of_students];
for (int i = 0; i < obj.No_Of_Students; i++)
{
students[i] = obj.students[i];
}
}
Course::~Course()//working of destructor
{
delete[] students;
}
string Course::get_Course_Name()
{
return Course_Name;
}
void Course::add_student(const string& name)
{
if (No_Of_Students < capacity_of_students)
{
students[No_Of_Students] = name;
No_Of_Students++;
}
else
{
cout << "We can not add more students beacuse the course is full." << endl;
}
}
void Course::drop_student(const string& name)
{
for (int i = 0; i < No_Of_Students; i++)
{
if (students[i] == name)
{
for (int j = i; j < No_Of_Students - 1; j++)
{
students[j] = students[j + 1];
}
No_Of_Students--;
return;
}
}
cout << "Student " << name << " not found in the course." << endl;
}
string* Course::get_student()
{
return students;
}
int Course::get_No_Of_Students()
{
return No_Of_Students;
}
int main()
{
Course c1("Object Oriented Programming", 20);
c1.add_student("Ahmed");
c1.add_student("Sara");
Course c2(c1); //using deep copy constructor
c2.drop_student("Ahmed");//dropping a student
cout << "Number of the students in course 1: " << c1.get_No_Of_Students() << endl;
string* students_c1 = c1.get_student();
for (int i = 0; i < c1.get_No_Of_Students() ; i++)
{
cout << students_c1[i] << " , ";
}
cout << endl;
cout << "Number of the students in course 2: " << c2.get_No_Of_Students() << endl;
string* students_c2 = c2.get_student();
for (int i = 0; i < c2.get_No_Of_Students(); i++)
{
cout << students_c2[i] << " , ";
}
cout << endl;
return 0;
}


