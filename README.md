# The-Data-Shelf
class Library:
    def __init__(self):
        self.books = {}  # Dictionary to store book details

    def add_book(self, title, author, copies):
        if title in self.books:
            self.books[title]['total'] += copies
            self.books[title]['available'] += copies
            print(f'Added {copies} more copies of "{title}".')
        else:
            self.books[title] = {
                'author': author,
                'total': copies,
                'available': copies
            }
            print(f'Book "{title}" added with {copies} copies.')

    def display_books(self):
        if not self.books:
            print("No books in library.")
        else:
            for title, info in self.books.items():
                print(f'{title} by {info["author"]} - Total: {info["total"]}, Available: {info["available"]}')

    def issue_book(self, title):
        if title in self.books:
            if self.books[title]['available'] > 0:
                self.books[title]['available'] -= 1
                print(f'One copy of "{title}" issued.')
            else:
                print("No available copies to issue.")
        else:
            print("Book not found in library.")

    def return_book(self, title):
        if title in self.books:
            if self.books[title]['available'] < self.books[title]['total']:
                self.books[title]['available'] += 1
                print(f'One copy of "{title}" returned.')
            else:
                print("All copies are already in the library.")
        else:
            print("Book not found in library.")

def main():
    library = Library()
    print("Welcome to the Library Management System")
    while True:
        print("\nOptions: 1-Add Book  2-Display Books  3-Issue Book  4-Return Book  5-Exit")
        choice = input("Enter choice: ")

        if choice == '1':
            title = input("Enter book title: ")
            author = input("Enter author name: ")
            try:
                copies = int(input("Enter number of copies: "))
                if copies > 0:
                    library.add_book(title, author, copies)
                else:
                    print("Number of copies must be positive.")
            except ValueError:
                print("Invalid number entered.")
        elif choice == '2':
            library.display_books()
        elif choice == '3':
            title = input("Enter book title to issue: ")
            library.issue_book(title)
        elif choice == '4':
            title = input("Enter book title to return: ")
            library.return_book(title)
        elif choice == '5':
            print("Exiting system. Goodbye!")
            break
        else:
            print("Invalid choice, try again.")

if __name__ == "__main__":
    main()
