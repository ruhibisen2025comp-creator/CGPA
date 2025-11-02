#include <stdio.h>
#include <string.h>
struct Student {
    char name[50];
    int roll;
    char contact[15];
    float cgpa;
    char grade;
    int rank;
};
char getGrade(float c) {
    if (c >= 9) return 'A';
    else if (c >= 8) return 'B';
    else if (c >= 7) return 'C';
    else if (c >= 6) return 'D';
    else return 'F';
}
int main() {
    struct Student s[50];
    int n, i, j;
    
    printf("Enter total number of students: ");
    if (scanf("%d", &n) != 1 || n <= 0) {
        printf("Error: Enter number only!\n");
        return 0;
    }
    for (i = 0; i < n; i++) {
        printf("\nStudent %d Details:\n", i + 1);
        printf("Roll No: ");
        if (scanf("%d", &s[i].roll) != 1) {
            printf("Error: Roll number must be numeric!\n");
            return 0;
        }
        printf("Name: ");
        scanf(" %[^\n]", s[i].name);

        printf("Contact No: ");
        scanf("%s", s[i].contact);
        if (strlen(s[i].contact) != 10) {
            printf("Error: Contact number must be 10 digits!\n");
            return 0;
        }
        printf("CGPA: ");
        if (scanf("%f", &s[i].cgpa) != 1 || s[i].cgpa < 0 || s[i].cgpa > 10) {
            printf("Error: Enter valid CGPA between 0–10!\n");
            return 0;
        }
        s[i].grade = getGrade(s[i].cgpa);
    }
    for (i = 0; i < n - 1; i++)
        for (j = i + 1; j < n; j++)
            if (s[i].cgpa < s[j].cgpa) {
                struct Student t = s[i];
                s[i] = s[j];
                s[j] = t;
            }
    for (i = 0; i < n; i++) {
        if (i > 0 && s[i].cgpa == s[i - 1].cgpa)
            s[i].rank = s[i - 1].rank;
        else
            s[i].rank = i + 1;
    }
    printf("\n--- Final Result ---\n");
    printf("Rank | Name\tRoll\tCGPA\tGrade\tContact\n");
    for (i = 0; i < n; i++)
        printf("%d\t%s\t%d\t%.2f\t%c\t%s\n", s[i].rank, s[i].name, s[i].roll, s[i].cgpa, s[i].grade, s[i].contact);

    printf("\nTopper: %s (CGPA: %.2f)\n", s[0].name, s[0].cgpa);
    return 0;
}

