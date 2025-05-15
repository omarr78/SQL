``` sql
create database Books;
GO

use Books;
GO

create schema Books_schema;


create table Books_schema.books_table(
	book_id int,
	book_title varchar(30) not null,
	book_author varchar(30) not null,
	book_topic varchar(30) not null,
	book_year int not null,
	constraint id_pk primary key (book_id),
	constraint title_uq unique (book_title),
	constraint year_chk check (book_year between 1900 AND 2025)
);

```
