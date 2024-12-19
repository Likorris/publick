#include <stdio.h>
#include <stdlib.h>

typedef struct Student {
    char Name[50];
    int Group;
    int Sess[5];
    struct Student *next;
} Student;

Student *head = NULL;

void addStudent(Student **head, char *name, int group, int Sess[]) {
    Student *newStudent = (Student*)malloc(sizeof(Student));
    int i = 0;
    while (name[i] != 0) {
        newStudent->Name[i] = name[i];
        i++;
    }
    newStudent->Name[i] = '\0';
    newStudent->Group = group;
    for (i = 0; i < 5; i++) {
        newStudent->Sess[i] = Sess[i];
    }
    newStudent->next = (*head);
    *head = newStudent;
}

void addStudentToEnd(Student *head) {
    Student *newStudent = (Student*)malloc(sizeof(Student));
    int i;
    printf("Введите фамилию и инициалы студента: ");
    scanf("%s", newStudent->Name);
    printf("Введите номер группы: ");
    scanf("%d", &newStudent->Group);
    printf("Введите 5 оценок через пробел: ");
    for (i = 0; i < 5; i++) {
        scanf("%d", &newStudent->Sess[i]);
    }
    newStudent->next = NULL;
    while (head->next != NULL) {
        head = head->next;
    }
    head->next = newStudent;
}

void addStudentAtPosition(Student *head) {
    Student *newStudent = (Student*)malloc(sizeof(Student));
    int i, position;
    printf("\nВведите позицию для добавления студента: ");
    scanf("%d", &position);

    printf("Введите фамилию и инициалы студента: ");
    scanf("%s", newStudent->Name);
    printf("Введите номер группы: ");
    scanf("%d", &newStudent->Group);
    printf("Введите 5 оценок через пробел: ");
    for (i = 0; i < 5; i++) {
        scanf("%d", &newStudent->Sess[i]);
    }
    Student *temp = head;
    for (i = 1; i < position - 1; i++) {
        temp = temp->next;
    }
    newStudent->next = temp->next;
    temp->next = newStudent;
}

void deleteStudentAtStart(Student **head) {
    Student *temp = *head;
    *head = (*head)->next;
    free(temp);
}

void deleteStudentAtEnd(Student *head) {
    Student *temp = head;
    while (temp->next->next != NULL) {
        temp = temp->next;
    }
    free(temp->next);
    temp->next = NULL;
}

void deleteStudentAtPosition(Student **head) {
    int position;
    printf("\nВведите позицию для удаления студента: ");
    scanf("%d", &position);
    Student *temp = *head;
    for (int i = 1; i < position - 1; i++) {
        temp = temp->next;
    }
    Student *tempr = temp->next;
    temp->next = tempr->next;
    free(tempr);
}

void displayStudents(const Student *head) {
    printf("Информация о студентах:\n");
    while (head) {
        printf("ФИО: %s, Группа: %d, Оценки: ", head->Name, head->Group);
        for (int i = 0; i < 5; i++) {
            printf("%d ", head->Sess[i]);
        }
        printf("\n");
        head = head->next;
    }
}

void displayStudentsWithFour(const Student *head) {
    while (head) {
        int sum = 0;
        for (int i = 0; i < 5; i++) {
            sum += head->Sess[i];
        }
        double average = (double)sum / 5;
        if (average > 4) {
            printf("Студенты со средним баллом выше четырех:\n");
            printf("ФИО: %s, Группа: %d, Средний балл: %.2f\n", head->Name, head->Group, average);
        }
        head = head->next;
    }
}


void displayStudentByNumber(const Student *head) {
int number; 
printf("Введите номер студента для вывода его данных: ");
scanf("%d", &number);
int numberofstudent = 1; 
while (head != NULL) {
if (numberofstudent == number) {
printf("ФИО: %s, Группа: %d, Оценки: ", head->Name, head->Group);
for (int i = 0; i < 5; i++) {
printf("%d ", head->Sess[i]);
}
printf("\n");
return;
}
head = head->next; 
numberofstudent++;
}
}

int saveToFile(struck nODE *head, const char *filename)(
    FILE *file = forep(filename, "wb");
    if (file == NULL)(
            printf("Ошибка при открытии файла\n");
            return -1;
    )
    struct Node *temp = head;
    while (temp != NULL);
        fwrite(&(temp->Person), sizeof(int Group), 1, file);
        temp = temp->next;
    )
    fclose(file);
    printf("Все студенты записаны в файл\n");
    return 0;
)

int loadFromFile(struct Node **head, const char *filename) (
    FILE *file = fopen(filename, "rb");
    if (file == NULL)(
        printf("Ошибка при открытии файла\n");
        return -1;
    )
    struct Group Person;
    while (fread(&Person, sizeof(struct Group), 1, file) == 1)(
        addStudentToEnd(head, person);
    )
    fclose(file);
    printf("Данные успешно загружены из файла. \n");
    return 0;
)
int main() {
char name[50];
int Sess[5];
int group;
int choice;
while (1) {
printf("Введите фамилию и инициалы студента (0 для завершения): ");
scanf("%s", name);
if (name[0] == '0') break;
printf("Введите номер группы: ");
scanf("%d", &group);
printf("Введите 5 оценок через пробел: ");
for (int i = 0; i < 5; i++) {
scanf("%d", &Sess[i]);
}
addStudent(&head, name, group, Sess);
}
displayStudents(head);
while (1) {

printf("\n1. Добавить студента в начало\n");
printf("2. Добавить студента в конец\n");
printf("3. Добавить студента на указанную позицию\n");
printf("4. Удалить студента из начала\n");
printf("5. Удалить студента с конца\n");
printf("6. Удалить студента с указанной позиции\n");
printf("7. Вывести всех студентов\n");
printf("8. Вывести студентов, у которых средний балл больше 4,0\n");
printf("9. Вывести студента по номеру\n");
printf("10. Выход\n");
printf("11. Записать значения в файл\n");
printf("12. Считать значения из файла\n");
printf("Выберите действие");
scanf("%d", &choice);
switch (choice) {
case 1:
printf("Введите фамилию и инициалы студента: ");
scanf("%s", name);
printf("Введите номер группы: ");
scanf("%d", &group);
printf("Введите 5 оценок через пробел: ");
for (int i = 0; i < 5; i++) {
scanf("%d", &Sess[i]);
}
addStudent(&head, name, group, Sess);
break;
case 2:
addStudentToEnd(head);
break;
case 3:
addStudentAtPosition(head);
break;
case 4:
deleteStudentAtStart(&head);
break;
case 5:
deleteStudentAtEnd(head);
break;
case 6:
deleteStudentAtPosition(&head);
break;
case 7:
displayStudents(head);
break;
case 8:
displayStudentsWithFour(head);
break;
case 9:
displayStudentByNumber(head);
break;
case 10:
exit(0);
case 11:

case 12:

default:
printf("Неверный выбор. Попробуйте снова.\n");
}
}
return 0;
}


