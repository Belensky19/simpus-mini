
# SIMPUS-Mini — UI/UX Wireframe

## 1. Tujuan
Dokumen ini merancang tampilan dan alur penggunaan SIMPUS-Mini
sebelum fitur baru diimplementasikan menggunakan kode.

## 2. Actors

### Guest
- Dapat melihat halaman Home.
- Dapat melihat katalog buku.
- Tidak perlu login untuk melihat katalog.

### Librarian
- Harus login untuk mengakses fitur petugas.
- Dapat mengelola buku dan anggota.
- Dapat melakukan transaksi peminjaman dan pengembalian.
- Dapat melihat riwayat transaksi.

## 3. Login Page

+--------------------------------------+
|             SIMPUS-Mini              |
|--------------------------------------|
|                                      |
|          [ Librarian Login ]         |
|                                      |
|   Username : [______________]        |
|   Password : [______________]        |
|                                      |
|             [ Sign In ]              |
|                                      |
+--------------------------------------+

## 4. Librarian Dashboard

+------------------------------------------------------------------+
| SIMPUS-Mini  Home | Books | Members | Loans | (Name) Logout      |
|------------------------------------------------------------------|
| [Total Books]     [Total Members]     [On Loan]                  |
|                                                                  |
| Quick Actions:                                                   |
| [ + New Loan ]       [ + Return ]                                |
|                                                                  |
| Recent Transactions                                              |
|------------------------------------------------------------------|
| Member | Book | Loan Date | Status                               |
+------------------------------------------------------------------+

## 5. Borrowing Page

+----------------------------------------------+
|              New Loan                        |
|----------------------------------------------|
| Member       : [Select Member________]        |
| Book         : [Select Available Book__]     |
| Loan Date    : [____________]                |
|                                              |
|                [ Save Loan ]                 |
+----------------------------------------------+

Business rule:
- Only books with stock greater than 0 can be selected.
- One book is selected per loan transaction.
- After a successful loan, book stock decreases by 1.

## 6. Returning Page

+----------------------------------------------+
|              Return Book                     |
|----------------------------------------------|
| Search active loan : [____________]           |
| Member             : [Loan Member]            |
| Book               : [Loan Book]              |
| Status             : [Not Returned]           |
|                                              |
|             [ Mark as Returned ]              |
+----------------------------------------------+

Business rule:
- Find an active loan before marking it as returned.
- After a successful return, book stock increases by 1.

## 7. History Page

+--------------------------------------------------------------+
|                    Transaction History                      |
|--------------------------------------------------------------|
| Search: [________________]  [Search]                         |
|--------------------------------------------------------------|
| Member | Book | Loan Date | Return Date | Status             |
|--------------------------------------------------------------|
|        |      |           |             |                    |
+--------------------------------------------------------------+

## 8. User Flow — Borrowing

[Librarian Login]
        |
        v
   [Dashboard]
        |
        v
 [Select New Loan]
        |
        v
   [Choose Member]
        |
        v
[Choose Book (stock > 0)]
        |
        v
      [Save]
        |
        v
[Book stock decreases by 1]
        |
        v
 [Back to Dashboard]

## 9. User Flow — Returning

   [Dashboard]
        |
        v
   [Select Return]
        |
        v
[Find active transaction]
        |
        v
 [Mark as Returned]
        |
        v
[Book stock increases by 1]
        |
        v
 [Back to Dashboard]

## 10. Authorisation

Guest:
- Can view Home and Book List.
- Cannot access librarian transaction features.

Librarian:
- Must log in before accessing protected features.
- Can access librarian dashboard and transaction features.

Note:
Authorisation requires program logic and cannot be enforced
by static HTML/CSS alone.

## 11. Edge Cases

1. A book with stock 0 must not be available for borrowing.
2. A member with overdue loans requires validation.
3. Returning a book must match an active loan.
4. A returned loan must not be returned a second time.

## 12. Consistency with Existing Design

- Reuse the existing navbar and responsive layout.
- Reuse the statistic cards from the existing dashboard.
- Reuse existing table and form styling in style.css.
- Add the Loans menu and login status indicator when implemented.
- Keep the same visual style across new pages.

## 13. Wireframe — Register New Member

+------------------------------------------+
|               SIMPUS-Mini                |
|------------------------------------------|
|                                          |
|           Register New Member            |
|                                          |
|   Full Name : [____________________]     |
|                                          |
|   Address   : [____________________]     |
|               [____________________]     |
|                                          |
|   Phone     : [____________________]     |
|                                          |
|   Email     : [____________________]     |
|                                          |
|             [ Register ]                 |
|                                          |
|   Already registered? [ Login ]          |
|                                          |
+------------------------------------------+

Actor: Guest

Purpose:
Allow a Guest to submit a request to register as a new member.

Fields:
- Full Name
- Address
- Phone
- Email

Primary action:
- Register

Secondary action:
- Login

Notes:
- This is a design wireframe, not a working registration form.
- Validation and data storage will be implemented in a later stage.

## 14. User Flow — Search Overdue Loans

[ Librarian Login ]
         |
         v
    [ Dashboard ]
         |
         v
 [ Open Loan History ]
         |
         v
 [ Select Overdue Filter ]
         |
         v
 [ Display Overdue Loans ]
         |
         v
 [ Select Member ]
         |
         v
 [ View Member Loan Details ]
         |
         v
 [ Review Overdue Books ]

Purpose:
Allow the librarian to find members whose loans are past
their due date.

Actor:
Librarian

Precondition:
The librarian has logged in.

Expected result:
The system displays overdue loan records and the relevant
member and book information.

## 15. Exercise — Additional Edge Cases

### Edge Case 1: Duplicate Loan
Scenario:
The librarian tries to lend the same book to the same member
twice in a row.

Expected behavior:
- The system checks the member's active loan records.
- The system warns the librarian if the same book is already
  on loan to that member.
- The librarian can review the existing transaction before
  creating another loan.

### Edge Case 2: Book Out of Stock
Scenario:
The librarian tries to borrow a book with stock equal to 0.

Expected behavior:
- The book cannot be selected in the loan form.
- The system displays a message that the book is unavailable.

### Edge Case 3: Overdue Loan
Scenario:
The member has an overdue loan.

Expected behavior:
- The system identifies the overdue loan.
- The librarian reviews the overdue record before proceeding
  with another transaction.

### Edge Case 4: Duplicate Return
Scenario:
The librarian tries to return a book that has already
been marked as returned.

Expected behavior:
- The system checks the loan status.
- A returned loan cannot be processed a second time.

### Edge Case 5: Invalid Loan Record
Scenario:
The librarian tries to return a book without a matching
active loan record.

Expected behavior:
- The system does not complete the return transaction.
- The librarian is asked to verify the loan information.

Note:
These are design-level rules. Their actual enforcement

requires program logic and is not provided by static HTML/CSS.
