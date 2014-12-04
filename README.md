#SQL Lab


##Getting Started

To get started we'll need to import the booktown.sql file.

1. open terminal
2. use the command `psql -f booktown.sql`
3. type `sql` to open your psql console
4. type \list to ensure the booktown database was successfully completed

##Instructions
Provide the follow sql statements below each question.


##Order
1. Find all subjects sorted by subject
SELECT * FROM subjects ORDER BY subject ASC;

2. Find all subjects sorted by location
SELECT * FROM subjects ORDER BY location ASC;


##Where
1. Find the book "Little Women"
SELECT * FROM books WHERE title = 'Little Women';

2. Find all books containing the word "Python"
SELECT * FROM books WHERE title ILIKE '%Python%';

3. Find all subjects with the location "Main St" sort them by subject
SELECT * FROM subjects WHERE location ILIKE '%Main St%' ORDER BY subject ASC;


##Joins

1. Find all books about Computers list ONLY book title
SELECT title FROM books
JOIN subjects ON subjects.id = subject_id
WHERE subject_id = 4;

* Find all books and display ONLY
	* Book title
	* Author's first name
	* Author's last name
	* Book subject
SELECT books.title, subjects.subject,
authors.first_name, authors.last_name
FROM authors
JOIN books ON books.author_id = authors.id
JOIN subjects ON books.subject_id = subjects.id;

* Find all books that are listed in the stock table
	* Sort them by retail price (most expensive first)
	* Display ONLY: title and retail price
SELECT books.title, stock.retail
FROM books
JOIN editions ON editions.book_id = books.id
JOIN stock ON stock.ISBN = editions.ISBN
ORDER BY stock.retail DESC;

* Find the book "Dune" and display ONLY
	* Book title
	* ISBN number
	* Publisher name
	* Retail price
SELECT books.title, editions.ISBN, stock.retail, publishers.name
FROM books
JOIN editions ON editions.book_id = books.id
JOIN stock ON stock.ISBN = editions.ISBN
JOIN publishers ON publishers.id = editions.publisher_id
WHERE books.title LIKE 'Dune';


* Find all shipments sorted by ship date display ONLY:
	* Customer first name
	* Customer last name
	* ship date
	* book title
SELECT customers.first_name, customers.last_name, shipments.ship_date, books.title
FROM customers
JOIN shipments ON shipments.customer_id = customers.id
JOIN editions ON editions.ISBN = shipments.ISBN
JOIN books ON books.id = editions.book_id
ORDER BY shipments.ship_date;

* Find all books that have either a 2nd or 3rd edition associated to it display ONLY:
	* Book title
	* Book Author
	* Edition Number
SELECT books.title, authors.first_name, authors.last_name, editions.edition
FROM books
JOIN editions ON editions.book_id = books.id
JOIN authors ON authors.id = books.author_id
WHERE editions.edition IN (2,3);
