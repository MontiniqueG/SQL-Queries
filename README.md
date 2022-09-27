# SQL-Queries
These are example of the SQL scripts I have written. I've been a data analyst for 3 years now, and I am just hearing about github. So, I have not saved all of my projects in the 3 years time frame. I am just starting to save a few scripts. 

1)	Write a query to return the following fields where StudentID = 4183909.
-	StudentID
-	FirstName
-	LastName
-	CellPhone
-	AcademicStatus (of Student record)
-	AcademicSubStatus (of Student record)

select StudentID
, FirstName
, LastName
, CellPhone
, A.Description AcademicStatus
, t.Description AcademicSubStatus
from Apus_pad.dbo.tblstudent S (nolock)
   join Apus_pad.dbo.tlkpAcademicStatus A (nolock) on S.CurrentAcademicStatusID = A.AcademicStatusID
   Left join Apus_pad.dbo.tlkpAcademicSubStatus T (nolock) on s.CurrentAcademicSubStatusID = T.AcademicSubStatusID
Where StudentID = '4183909'

2.) Write a query to show the relationship between Academic Status and AcademicSubStatus.
-	AcademicStatusID
-	Description  (AcademicStatus)
-	Status (AcademicStatus)
-	AcademicSubStatusID
-	Description (AcademicSubStatus)
-	Status (AcademicSubStatus)

select S.AcademicStatusID
, S.Description
, S.Status
, A.AcademicSubStatusID
, A.Description
, A.Status
from Apus_pad.dbo.tlkpAcademicStatus S
left join Apus_pad.dbo.tlkpAcademicSubStatus A on s.AcademicStatusID = A.AcademicStatusID

3.) Write a query to show the Active and Primary program type and program name where StudentID = 4183909.
-	StudentID
-	FirstName
-	LastName
-	AcademicStatus (of Degree record)
-	AcademicSubStatus (of Degree record)
-	ProgramType
-	ProgramName


select s.StudentID
, s.FirstName
, s.LastName
, A.Description AcademicStatus
, T.Description AcademicSubStatus
, d.studentdegreeid
, p3.program_name ProgramName
, pt.type_name ProgramType
, d.isactive
, g.IsPrimary
from Apus_pad.dbo.tblstudent S (nolock)

join Apus_pad.dbo.tblstudentdegree D (nolock) on S.StudentID = D.studentid
join Apus_pad.dbo.xdegreeprogram G (nolock) on D.studentdegreeid = G.student_degree_id
join Apus_pad.dbo.program3archive P (nolock) on G.program_archive_id = P.program_archive_id
join Apus_pad.dbo.program3 P3 (nolock) on p.program_id = P3.program_id
join Apus_pad.dbo.lprogramtypes PT (nolock) on p3.program_type_id = PT.program_type_id
join Apus_pad.dbo.tlkpAcademicStatus A (nolock) on D.academicstatus = A.AcademicStatusID
left join Apus_pad.dbo.tlkpAcademicSubStatus T (nolock) on  d.academicSubstatusId = T.AcademicSubStatusID
Where s.StudentID = '4183909'
--and d.isactive = 1
--and g.IsPrimary = 1
