Лаборатори №5: API системийн тест – Postman ба Newman

Оюутны мэдээлэл

Нэр: ANAR BATBOLD

Оюутны код: B170910823

Хичээл: F.CSA313 Программ хангамжийн чанарын баталгаа ба тест

Ашигласан хэрэгслүүд

Node.js

Postman

Newman

GitHub

Туршилтын систем

Энэхүү лабораторийн ажлаар хичээл бүртгэлийн REST API системийг тестэлсэн.



Систем нь дараах endpoint-уудтай.



Students

PUT /students/:id

Courses

PUT /courses/:id

GET /courses/:id

Registrations

POST /registrations

GET /registrations

Тестийн сценарионууд

Эерэг тестүүд

Create Student

Create Course

Create Registration

Get Registrations

Get Course

Сөрөг тестүүд

Register Unknown Student

Register Unknown Course

Register Missing Prerequisite

Infrastructure тест

Server Down Scenario

PASS Scenario

Create Student

{

&#x20; "result": "OK"

}

Create Course

{

&#x20; "result": "OK"

}

Create Registration

{

&#x20; "result": "OK",

&#x20; "registrationID": 2

}

Get Registrations

\[

&#x20; {

&#x20;   "registrationID": 1,

&#x20;   "studentID": "B231234567",

&#x20;   "courseID": "CS313"

&#x20; },

&#x20; {

&#x20;   "registrationID": 2,

&#x20;   "studentID": "B231234567",

&#x20;   "courseID": "CS313"

&#x20; }

]

Newman PASS Run

iterations executed: 1

iterations failed: 0



assertions executed: 20

assertions failed: 0

PASS Үр Дүн

Үзүүлэлт	Утга

Assertions	20

Failed Assertions	0

Iterations	1

Failed Iterations	0

Бүх assertion амжилттай ажилласан.



FAIL Scenario

FAIL тест хийхийн тулд нэг assertion-ыг зориудаар өөрчилсөн.



Анхны assertion

pm.expect(pm.response.json().result).to.eql("OK");

Өөрчилсөн assertion

pm.expect(pm.response.json().result).to.eql("SUCCESS");

Бодит response:



{

&#x20; "result": "OK"

}

учир assertion зориудаар FAIL болсон.



Newman FAIL Run

assertions executed: 20

assertions failed: 1

FAIL Үр Дүн

Үзүүлэлт	Утга

Assertions	20

Failed Assertions	1

Энэ нь Newman буруу хүлээлтийг амжилттай илрүүлж байгааг харуулсан.



Server Down Scenario

Серверийг зогсоосны дараа Collection-ийг Newman ашиглан дахин ажиллуулсан.



Үр Дүн

connect ECONNREFUSED 127.0.0.1:3000

алдаа олон удаа бүртгэгдсэн.



Тайлбар

API сервер унтарсан үед Newman хүсэлтүүдийг гүйцэтгэж чадалгүй:



ECONNREFUSED

алдаа гаргасан.



Энэ нь системийн дэд бүтэц болон холболтын асуудлыг илрүүлэх боломжтойг харуулсан.



API Error Scenario-ууд

ERROR\_NO\_STUDENT

Request

{

&#x20; "studentID": "UNKNOWN",

&#x20; "courseID": "CS313"

}

Response

{

&#x20; "result": "ERROR\_NO\_STUDENT"

}

ERROR\_NO\_COURSE

Request

{

&#x20; "studentID": "B231234567",

&#x20; "courseID": "UNKNOWN"

}

Response

{

&#x20; "result": "ERROR\_NO\_COURSE"

}

ERROR\_PREREQUISITES

Request

{

&#x20; "studentID": "B000000001",

&#x20; "courseID": "CS313"

}

Response

{

&#x20; "result": "ERROR\_PREREQUISITES",

&#x20; "missing": \[

&#x20;   "CS201"

&#x20; ]

}

Энэ туршилт нь prerequisite шалгалт зөв ажиллаж байгааг баталсан.



Newman Results Summary

PASS Run

Үзүүлэлт	Утга

Assertions	20

Failed	0

FAIL Run

Үзүүлэлт	Утга

Assertions	20

Failed	1

DOWN Run

Үзүүлэлт	Утга

Network Error	ECONNREFUSED

Дүгнэлт

Энэхүү лабораторийн ажлаар REST API системийг Postman болон Newman ашиглан тестэллээ. API-ийн үндсэн бизнес үйлдлүүд болох оюутан үүсгэх, хичээл үүсгэх, хичээлд бүртгүүлэх болон бүртгэлийн жагсаалт авах үйлдлүүдийг шалгасан. Мөн оюутан байхгүй, хичээл байхгүй болон prerequisite хангагдаагүй нөхцөлүүдийг туршиж бизнес дүрмүүд зөв хэрэгжиж байгааг баталгаажуулсан. Postman ашиглан request болон response-уудыг шалгаж assertion-ууд үүсгэсэн. Newman ашиглан collection-ийг автоматаар ажиллуулж API тестийг командын мөрөөс гүйцэтгэсэн. PASS run үед бүх 20 assertion амжилттай болсон. FAIL run үед зориудаар өөрчилсөн assertion алдаа илрүүлж 1 failure бүртгэсэн. Server Down scenario үед Newman ECONNREFUSED алдааг илрүүлсэн. Энэ нь зөвхөн функциональ тест төдийгүй системийн найдвартай ажиллагааг шалгах боломжтойг харуулсан. Лабораторийн ажлын үр дүнд Postman Collection болон Newman Automation ашиглан API системийн тестийг хэрэгжүүлж сурлаа.



Хавсаргасан файлууд

server.js



lab05-collection.json

lab05-collection-fail.json



results/newman-pass.txt

results/newman-fail.txt

results/newman-down.txt

