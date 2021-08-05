create table marks (
	course varchar(5),
    assignnum SMALLINT,
    studnum int,
    1stmark SMALLINT CHECK(1stmark >= 0 AND 1stmark <= 10),
    2rdmark SMALLINT CHECK(2rdmark >= 0 AND 2rdmark <= 10),
    PRIMARY KEY(course)
)

======================================================================================

CREATE TABLE students(
    studnum INT,
    surname VARCHAR(20),
    firstname VARCHAR(6) CHECK
        (LENGTH(firstname) >= 5),
        address VARCHAR(40),
        birthdate DATE
    CHECK
        (YEAR(birthdate) > 2000),
        gender TINYINT(1),
        PRIMARY KEY(studnum)
)

======================================================================================

ALTER TABLE marks
ADD FOREIGN KEY (studnum) REFERENCES students(studnum);

======================================================================================

INSERT INTO students(
    `studnum`,
    `surname`,
    `firstname`,
    `address`,
    `birthdate`,
    `gender`
)
VALUES(
    1,
    'long',
    'nguyen',
    '123 ngsuyen chi cong',
    '2001-07-10',
    1
),(
    2,
    'longs',
    'nguyena',
    '123 ngasdfuyen chi cong',
    '2001-05-11',
    0
),(
    3,
    'longd',
    'nguyens',
    '12s3 nguyasdggfhen chi cong',
    '2001-02-12',
    1
),(
    4,
    'longf',
    'nguyenf',
    '12d3 nguyen chi csdong',
    '2001-01-23',
    0
),(
    5,
    'longh',
    'nguyenk',
    '12r3 nguyen chisss cong',
    '2001-12-22',
    1
)

======================================================================================

INSERT INTO marks(
    `course`,
    `assignnum`,
    `studnum`,
    `1stmark`,
    `2rdmark`
)
VALUES('toan', 1, 1, 5, 7),('ly', 2, 2, 5, 7),('hoa', 3, 3, 5, 7),('van', 4, 4, 5, 7),('anh', 5, 5, 5, 7)

======================================================================================

CREATE VIEW infoStud AS
    SELECT
        marks.*, 
        students.`surname`,students.`firstname`,students.`address`,students.`birthdate`,students.`gender`
    FROM
        students INNER JOIN marks ON students.studnum = marks.studnum
    GROUP by students.studnum;

======================================================================================

CREATE PROCEDURE studentInfo(IN MaSV INT)
SELECT
    students.studnum,
    students.firstname,
    students.surname,
    students.address,
    students.birthdate,
    students.gender,
    marks.course,
    marks.assignnum,
    marks.1stmark,
    marks.2rdmark
FROM
    students
INNER JOIN marks ON students.studnum = marks.studnum
WHERE
    students.studnum = MaSV
