#include <iostream>
#include <string>
#include <stack>
using namespace std;

int main() {
    const int MAX = 100;
    int ids[MAX];
    string booknames[MAX];
    string authors[MAX];
    int size = 0;

    stack<int> deletedBooks;
    int choice;

    do {
       cout << "\n library data manager   1. add book   2. delete book  3. undo delete 4. search book 5. display all books 0. exit\n";
        cout << "enter your choice ";
        cin >> choice;

        if (choice == 1) {
            if (size < MAX) {
                cout << "enter book id ";
                cin >> ids[size];
                cout << "enter book title ";
                cin >> booknames[size];
                cout << "enter author ";
                cin >> authors[size];
                size++;
                cout << "book added successfully\n";
            } else {
                cout << "library is full\n";
            }
        }
        else if (choice == 2) {
            if (size > 0) {
                int delId;
                cout << "enter book id to delete ";
                cin >> delId;
                int found = 0;
                for (int i = 0; i < size; i++) {
                    if (ids[i] == delId) {
                        deletedBooks.push(ids[i]);
                        for (int j = i; j < size - 1; j++) {
                            ids[j] = ids[j + 1];
                            booknames[j] = booknames[j + 1];
                            authors[j] = authors[j + 1];
                        }
                        size--;
                        cout << "book deleted\n";
                        found = 1;
                        break;
                    }
                }
                if (!found) cout << "book id not found\n";
            } else {
                cout << "no books to delete\n";
            }
        }
        else if (choice == 3) {
            if (!deletedBooks.empty() && size < MAX) {
                int restoredId = deletedBooks.top();
                deletedBooks.pop();
                ids[size] = restoredId;
                cout << "enter book title ";
                cin >> booknames[size];
                cout << "enter author ";
                cin >> authors[size];
                size++;
                cout << "undo delete successful\n";
            } else {
                cout << "no deleted book to undo\n";
            }
        }
        else if (choice == 4) {
            int searchId;
            cout << "enter book id to search ";
            cin >> searchId;
            bool found = false;
            for (int i = 0; i < size; i++) {
                if (ids[i] == searchId) {
                    cout << "book found\n";
                    cout << "id " << ids[i] << " ";
                    cout << "title " << booknames[i] << " ";
                    cout << "author " << authors[i] << "\n";
                    found = true;
                    break;
                }
            }
            if (!found) cout << "book not found\n";
        }
        else if (choice == 5) {
            if (size == 0) {
                cout << "no books available\n";
            } else {
                cout << "\nid     title     author\n";
                for (int i = 0; i < size; i++) {
                    cout << ids[i] << "     " << booknames[i] << "     " << authors[i] << "\n";
                }
            }
        }
    } while (choice != 0);

    return 0;
}
