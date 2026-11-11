# Library Management System (Core Java)

A console-based library system where students request books and a librarian approves issues, collects fines and generates reports.

## Workflow
```
Student requests book -> Librarian approves -> Book is issued (due in 14 days)
Student returns book  -> Fine calculated if late -> Librarian collects fine
```

## Features

**Student menu**
- Search a book by title or author
- View book availability
- Request a book issue (needs librarian approval)
- Return a book (fine is calculated automatically)
- View my issued books and pending fine

**Librarian menu** (password: `admin123`)
- Add books
- Approve or reject issue requests
- Collect fines (full or partial payment)
- Generate reports
- Book availability
- Fine calculator
- Due date reminders (books due within 2 days, or overdue)
- Change system date (simulation, for testing late returns)

## Rules
| Rule | Value |
|------|-------|
| Loan period | 14 days |
| Fine | Rs.5 per day after the due date |
| Max books per student | 3 |
| Pending fine | Must be cleared before requesting a new book |

## Concepts Covered
| Concept | Where it is used |
|---------|------------------|
| Classes and objects | `Book`, `IssueRecord`, `IssueRequest`, `Library`, `Main` |
| ArrayList | `List<Book>` stores all books, `List<IssueRequest>` stores pending requests |
| HashMap | `Map<String, IssueRecord>` issued books (bookId -> record), `Map<String, Double>` pending fines (studentId -> amount) |
| Date handling (LocalDate) | Issue date, due date, `ChronoUnit.DAYS` for late days |
| Exception handling | Custom `LibraryException` (book not found, already issued, limit reached, and so on) |

## Project Structure
```
2_LibraryManagement/
  Main.java      (Book, IssueRecord, IssueRequest, LibraryException, Library, Main)
  README.md
```

## How to Run
Requires JDK 17 or newer.
```
cd 2_LibraryManagement
javac Main.java
java Main
```

## Sample Walkthrough
1. **Student menu**: enter your student ID (for example `S1`), choose **Request book issue**, enter `B101`.
2. **Librarian menu** (password `admin123`): choose **Approve / reject issue requests**, pick request 1, enter `A`.
3. **Librarian menu**: choose **Change system date** and enter a date 20 days ahead (format `yyyy-MM-dd`). Then choose **Due date reminders** to see the overdue warning.
4. **Student menu**: choose **Return book**, enter `B101`. A fine is added (6 late days x Rs.5 = Rs.30).
5. **Librarian menu**: choose **Collect fine**, enter the student ID and the amount.
6. **Librarian menu**: choose **Generate report** to see totals.

## Preloaded Books
| ID | Title | Author |
|----|-------|--------|
| B101 | Core Java | Herbert Schildt |
| B102 | Effective Java | Joshua Bloch |
| B103 | Clean Code | Robert C. Martin |
| B104 | Data Structures | Mark Allen Weiss |
| B105 | Operating Systems | Galvin |

## Notes and Limitations
- Data is stored **in memory only** and is lost when the program exits.
- The librarian password is hard-coded as `admin123`. Change `LIBRARIAN_PASSWORD` in `Main.java`.
- Only one pending request is allowed per book at a time.
- Students are identified by the ID they type. There is no student login.

## Possible Improvements
- Save books and records to a file or database
- Student registration and login
- Reservation queue for books that are already issued
- Email or SMS due-date reminders

# Online Voting System (Core Java)

A console-based college election system where students register, log in and vote digitally. **Each student can vote only once.**

## Features
- Register / Login (users stored in a `HashMap`)
- View candidate list
- Cast a vote (duplicate voting is blocked)
- View total votes per candidate
- Result display: **Finalist (winner)** is picked automatically, plus the **Runner-Up**
- Tie handling: if the top spots are tied, the result says so and recommends a re-election

## Concepts Covered
| Concept | Where it is used |
|---------|------------------|
| OOP | `User`, `Candidate`, `VotingService`, `Main` classes |
| Collections (HashMap) | `Map<String, User>` users, `Map<String, Boolean>` voted-or-not, `Map<String, Integer>` candidate votes |
| Exception handling | Custom `VotingException` (duplicate username, wrong password, double vote, invalid candidate) |

## Logic Design
```
Map<String, User>     users      -> username  -> User
Map<String, Boolean>  hasVoted   -> username  -> has this user voted?
Map<String, Integer>  votes      -> candidate -> vote count
```

## Project Structure
```
1_VotingSystem/
  Main.java      (VotingException, User, Candidate, VotingService, Main)
  README.md
```

## How to Run
Requires JDK 17 or newer.
```
cd 1_VotingSystem
javac Main.java
java Main
```

## Sample Walkthrough
1. Choose **1. Register** and enter your name, a username and a password.
2. Choose **2. Login & Vote**, log in, then enter the ID of the candidate you want.
3. Try voting again with the same user: you will see an error, because only one vote is allowed.
4. Choose **4. View Total Votes** to see the count per candidate.
5. Choose **5. Show Result** to see the Finalist and Runner-Up.

Example result output:
```
========== ELECTION RESULT ==========
FINALIST (WINNER) : Aarav Sharma with 5 votes
RUNNER-UP         : Diya Menon with 3 votes
=====================================
```

## Preloaded Candidates
| ID | Name | Position |
|----|------|----------|
| 1 | Aarav Sharma | President |
| 2 | Diya Menon | President |
| 3 | Rohan Gupta | President |
| 4 | Sneha Iyer | President |

To change them, edit the `addCandidate(...)` lines at the top of `main()` in `Main.java`.

## Notes and Limitations
- Data is stored **in memory only**. Users and votes are lost when the program exits.
- Passwords are stored as plain text for simplicity. A real system should hash them.
- If no votes are cast, the result screen shows an error instead of a winner.
- If no other candidate received votes, the runner-up shows as "none".

## Possible Improvements
- Save users and votes to a file or database
- Add an admin login to open and close voting
- Hash passwords
- Support multiple positions (President, Secretary, and so on)
