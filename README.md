# CourseSelection_WPF
Course Selection Application

A Console & WPF Application for Selecting Courses

Project Overview:
This repository contains two versions of a Course Selection Application:
    1.    Console Application – A simple text-based interface for selecting courses.
    2.    WPF Application – A graphical user interface (GUI) version for an improved user experience.

Both versions demonstrate my ability to work with existing code, implement changes based on software requirements, and develop user-friendly applications.

Project Goals & User Needs:
The goal of this application is to help students efficiently select courses based on available options, limit credit hours, and avoid double submissions.

This project meets the following user needs:
    •    Allows users to view available courses.
    •    Enables users to filter courses based on requirements.
    •    Helps users plan their schedules efficiently.
    •    Provides a clear and user-friendly interface (Console & WPF versions).

Key Features:
Console Application
    •    Displays available courses in a text-based format.
    •    Allows user input to select courses.
    •    Basic error handling for invalid selections.
WPF Application
    •    Interactive UI with buttons and dropdowns.
    •    More visual feedback for users selecting courses.
    •    Improved navigation for better user experience.

Development Process & Challenges:
What I Did Well
    •    Successfully implemented code changes based on requirements.
    •    Designed a clear and structured UI in the WPF version.
    •    Followed best practices for code readability & maintainability.

Console vs. WPF Design:
Feature    Console Application    WPF Application
User Interface    Text-based    Graphical (Buttons, Lists)
Navigation    Command-line input    Mouse clicks & UI controls
Error Handling    Simple text prompts    Validation with UI feedback
User Experience    Basic, functional    More intuitive & engaging

Debugging & Problem-Solving:
To ensure smooth functionality, I used the following debugging techniques:
    •    Breakpoints & Step through Debugging in Visual Studio.
    •    Error Logging to catch invalid inputs.
    •    Unit Testing to verify functionality.

Future Use:
These debugging strategies can be applied to larger projects to enhance efficiency and catch errors early.

Screenshots & Source Code
WPF Screenshots: 
![Peinado_Screenshot1_WPFRegisterStudent](https://github.com/user-attachments/assets/175c93b6-7002-4f9a-a6bf-6b87e7326d57)
![Peinado_Screenshot2_WPFRegisterStuden](https://github.com/user-attachments/assets/79531391-27d3-4ee0-ba7a-b904c5993b12)
![Peinado_Screenshot3_WPFRegisterStuden](https://github.com/user-attachments/assets/62995362-251b-4354-9229-32851a39abc6)
![Peinado_Screenshot4_WPFRegisterStuden](https://github.com/user-attachments/assets/d32ca482-560e-4d90-b025-52ecf1dc5aed)
![Peinado_Screenshot5_WPFRegisterStuden](https://github.com/user-attachments/assets/fb444bea-d636-4d26-acaf-23f06c73048e)
![Peinado_Screenshot6_WPFRegisterStuden](https://github.com/user-attachments/assets/e26a6da2-5662-4b24-bbe4-9b4237ca4434)
![Peinado_Screenshot7_WPFRegisterStuden](https://github.com/user-attachments/assets/014ec57b-9097-4b4b-8e1f-ecc411503bbb)

WFP Source code: 
MainWindow.xaml.cs Source code: 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace WPFRegisterStudent
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private List<Course> courses;
        private int totalCreditHours = 0;
        private const int MAX_CREDIT_HOURS = 9;

        public MainWindow()
        {
            InitializeComponent();
        }

        private void Window_Loaded(object sender, RoutedEventArgs e)
        {

            courses = new List<Course>
            {
                new Course("IT 145", 3),
                new Course("IT 200", 3),
                new Course("IT 201", 3),
                new Course("IT 270", 3),
                new Course("IT 315", 3),
                new Course("IT 328", 3),
                new Course("IT 330", 3),
            };

            foreach (Course course in courses)
            {
                comboBox.Items.Add(course);
            }

            textBox.Text = "0";
        }

        private void button_Click(object sender, RoutedEventArgs e)
        {
            if (comboBox.SelectedItem == null)
            {
                MessageBox.Show("Please select a course to register.", "Selection Error", MessageBoxButton.OK, MessageBoxImage.Warning);
                return;
            }

            Course selectedCourse = (Course)comboBox.SelectedItem;

            if (selectedCourse.IsRegisteredAlready())
            {
                MessageBox.Show("You are already registered for this course.", "Registration Error", MessageBoxButton.OK, MessageBoxImage.Error);
                return;
            }

            if (totalCreditHours + selectedCourse.GetCreditHours() > MAX_CREDIT_HOURS)
            {
                MessageBox.Show("Registration failed: Maxmimum allowed credit hours (9) exceeded.", "Credit Hour Limit Reached", MessageBoxButton.OK, MessageBoxImage.Warning);
                return;
            }

            selectedCourse.SetToRegistered();

            totalCreditHours += selectedCourse.GetCreditHours();

            textBox.Text = $"{totalCreditHours}";

            listBox.Items.Add(selectedCourse.getName());

            MessageBox.Show($"You have successfully registered for {selectedCourse.getName()}!", "Registration Successful", MessageBoxButton.OK, MessageBoxImage.Information);

        }

    }
}

Course.cs source code: 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace WPFRegisterStudent
{
    class Course
    {
        private string name;
        private bool isRegisteredAlready;
        private int creditHours;

        public Course(string name, int creditHours)
        {
            this.name = name;
            this.creditHours = creditHours;
            this.isRegisteredAlready = false;
        }

        public string getName()
        {
            return name;
        }

        public bool IsRegisteredAlready()
        {
            return isRegisteredAlready;
        }

        public void SetToRegistered()
        {
            isRegisteredAlready = true;
        }

        public int GetCreditHours()
        {
            return creditHours;
        }

        public override string ToString()
        {
            return $"{getName()} - {creditHours} Credit Hours";
        }
    }
}

Console Screenshots: 
![Peinado_CRS_1st_Screenshot](https://github.com/user-attachments/assets/793dd416-844b-4c0f-943a-772d3c73b74b)
![Peinado_CRS_2nd_Screenshot](https://github.com/user-attachments/assets/746ecfd6-eec0-4fad-a21b-e7bbdd65bbcb)
![Peinado_CRS_3rd_Screenshot](https://github.com/user-attachments/assets/40f810d6-3037-45cb-924c-8794a74464c9)
![Peinado_CRS_4th_Screenshot](https://github.com/user-attachments/assets/cd81990b-6047-40b1-8c99-f88ef3554193)
![Peinado_CRS_5th_Screenshot](https://github.com/user-attachments/assets/49fd15b2-ccf9-4c66-8748-aca37166e3cf)
![Peinado_CRS_6th_Screenshot](https://github.com/user-attachments/assets/b8b26980-383d-4b13-b9ea-e0fe673b753d)
![Peinado_CRS_7th_Screenshot](https://github.com/user-attachments/assets/3488b767-bc66-4bea-bc34-8a797811fdec)

Console Source Code: 
Source code text: 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleRegisterStudent
{
    class Program
    {
        static void Main(string[] args)
        {
            (new Program()).run();
        }


        void run()
        {
            int choice;
            int firstChoice = 0, secondChoice = 0, thirdChoice = 0;
            int totalCredit = 0;
            string yesOrNo = "";

            Console.WriteLine("Peinado Copy");

            do
            {
                WritePrompt();
                choice = Convert.ToInt32(Console.ReadLine());

                switch (ValidateChoice(choice, firstChoice, secondChoice, thirdChoice, totalCredit))
                {
                    case -1:
                        Console.WriteLine("Your entered selection {0} is not a recognized course.", choice);
                        break;
                    case -2:
                        Console.WriteLine("You have already registerd for this {0} course.", ChoiceToCourse(choice));
                        break;
                    case -3:
                        Console.WriteLine("You can not register for more than 9 credit hours.");
                        break;
                    case 0:
                        Console.WriteLine("Registration Confirmed for course {0}.", ChoiceToCourse(choice));
                        totalCredit += 3;
                        if (firstChoice == 0)
                            firstChoice = choice;
                        else if (secondChoice == 0)
                            secondChoice = choice;
                        else if (thirdChoice == 0)
                            thirdChoice = choice;
                        break;
                }

                WriteCurrentRegistration(firstChoice, secondChoice, thirdChoice);
                Console.Write("\nDo you want to try again? (Y|N)? : ");
                yesOrNo = (Console.ReadLine()).ToUpper();
            } while (yesOrNo == "Y");

            Console.WriteLine("Thank you for registering with us");
        }

        void WritePrompt()
        {
            Console.WriteLine("Please select a course for which you want to register by typing the number inside []");
            Console.WriteLine("[1]IT 145\n[2]IT 200\n[3]IT 201\n[4]IT 270\n[5]IT 315\n[6]IT 328\n[7]IT 330");
            Console.Write("Enter your choice : ");
        }

        int ValidateChoice(int choice, int firstChoice, int secondChoice, int thirdChoice, int totalCredit)
        {
            if (choice < 1 || choice > 7)
                return -1;
            else if (choice == firstChoice || choice == secondChoice || choice == thirdChoice)
                return -2;
            else if (totalCredit + 3 > 9)
                return -3;
            return 0;
        }


        void WriteCurrentRegistration(int firstChoice, int secondChoice, int thirdChoice)
        {
            if (firstChoice == 0)
                Console.WriteLine("You have not registered for any courses yet.");
            else if (secondChoice == 0)
                Console.WriteLine("You are currently registered for {0}", ChoiceToCourse(firstChoice));
            else if (thirdChoice == 0)
                Console.WriteLine("You are currently registered for {0}, {1}", ChoiceToCourse(firstChoice), ChoiceToCourse(secondChoice));
            else
                Console.WriteLine("You are currently registered for {0}, {1}, {2}", ChoiceToCourse(firstChoice), ChoiceToCourse(secondChoice), ChoiceToCourse(thirdChoice));
        }

        string ChoiceToCourse(int choice)
        {
            switch (choice)
            {
                case 1: return "IT 145";
                case 2: return "IT 200";
                case 3: return "IT 201";
                case 4: return "IT 270";
                case 5: return "IT 315";
                case 6: return "IT 328";
                case 7: return "IT 330";
                default: return "Unknown Course";
            }
        }
    }
}

Conclusion:
These projects highlight my ability to develop both console and graphical applications, debug effectively, and design a user-friendly course selection system. It serves as a great addition to my portfolio, showcasing my skills in C#, UI design, and problem-solving.




