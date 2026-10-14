\# Лаборатори №5: API системийн тест – Postman ба Newman



\## Оюутны мэдээлэл



\- Нэр: ANAR BATBOLD

\- Код: B170910823

\- Хичээл: F.CSA313 Программ хангамжийн чанарын баталгаа ба тест



\---



\## Ашигласан орчин



\### Node.js



```text

v24.19.0

```



\### Newman



```text

6.2.2

```



\### Ашигласан хэрэгслүүд



\- Node.js

\- Postman

\- Newman

\- Git

\- GitHub



\---



\# Туршилтын систем



Систем нь хичээл бүртгэлийн REST API юм.



\### Endpoint-ууд



```http

PUT /students/:id

PUT /courses/:id

GET /courses/:id

POST /registrations

GET /registrations

```



\---



\# Сонголт ба төлөөлөх утгууд



| Параметр | Утга |

|----------|----------|

| Student | Valid, Unknown |

| Course | Valid, Unknown |

| Student Status | Active, Inactive |

| Prerequisite | Satisfied, Missing |

| Server | Running, Down |



\---



\# Спецификацийн хүснэгт



| # | Student | Course | Status | Prerequisite | Expected Result |

|---|---|---|---|---|---|

| 1 | Valid | Valid | Active | Satisfied | OK |

| 2 | Unknown | Valid | Active | Satisfied | ERROR\_NO\_STUDENT |

| 3 | Valid | Unknown | Active | Satisfied | ERROR\_NO\_COURSE |

| 4 | Valid | Valid | Active | Missing | ERROR\_PREREQUISITES |

| 5 | Valid | Valid | Active | Satisfied | Registration Created |

| 6 | Valid | Valid | Active | Satisfied | Registration List Returned |

| 7 | Valid | Valid | Active | Satisfied | Course Returned |

| 8 | Valid | Valid | Active | Satisfied | Newman PASS Run |

| 9 | Valid | Valid | Active | Satisfied | Server DOWN Scenario |



\---



\# Collection-д хэрэгжүүлсэн тестүүд



\### Эерэг тестүүд



1\. Create Student

2\. Create Course

3\. Create Registration

4\. Get Registrations

5\. Get Course



\### Сөрөг тестүүд



6\. Register Unknown Student

7\. Register Unknown Course

8\. Register Missing Prerequisite



\### Дэд бүтцийн тест



9\. Server DOWN Scenario



\---



\# PASS ажиллуулалт



\## Create Student



```json

{

&#x20; "result": "OK"

}

```



\## Create Course



```json

{

&#x20; "result": "OK"

}

```



\## Create Registration



```json

{

&#x20; "result": "OK",

&#x20; "registrationID": 2

}

```



\## Get Registrations



```json

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

```



\### Newman PASS Run



```text

Iterations executed: 1

Iterations failed: 0



Assertions executed: 20

Assertions failed: 0

```



\### Exit Code



```text

0

```



PASS ажиллуулалтын үед бүх assertion амжилттай болсон.



\---



\# FAIL ажиллуулалт



FAIL хувилбарт дараах assertion зориудаар өөрчилсөн.



Анхны assertion:



```javascript

pm.expect(pm.response.json().result).to.eql("OK");

```



Өөрчилсөн assertion:



```javascript

pm.expect(pm.response.json().result).to.eql("SUCCESS");

```



Бодит response:



```json

{

&#x20; "result": "OK"

}

```



учир assertion FAIL болсон.



\### Newman FAIL Run



```text

Assertions executed: 20

Assertions failed: 1

```



\### Exit Code



```text

1

```



Энэ нь Newman алдаатай expectation-ийг зөв илрүүлж байгааг харуулсан.



\---



\# Server DOWN ажиллуулалт



Серверийг зогсоосны дараа collection-ийг дахин ажиллуулсан.



\### Үр дүн



```text

connect ECONNREFUSED 127.0.0.1:3000

```



\### Exit Code



```text

1

```



Сервер ажиллахгүй үед Newman хүсэлтүүдийг гүйцэтгэж чадахгүй байсныг харуулсан.



\---



\# Oracle алдаа ба Infrastructure алдаа



\## Oracle / Business Rule Errors



Дараах алдаанууд нь системийн бизнес дүрэмтэй холбоотой.



```text

ERROR\_NO\_STUDENT

ERROR\_NO\_COURSE

ERROR\_PREREQUISITES

```



Эдгээр нь API ажиллаж байгаа боловч хэрэглэгчийн өгсөн өгөгдөл бизнес дүрэм зөрчсөн үед буцаж байна.



\### ERROR\_NO\_STUDENT



```json

{

&#x20; "result": "ERROR\_NO\_STUDENT"

}

```



\### ERROR\_NO\_COURSE



```json

{

&#x20; "result": "ERROR\_NO\_COURSE"

}

```



\### ERROR\_PREREQUISITES



```json

{

&#x20; "result": "ERROR\_PREREQUISITES",

&#x20; "missing": \[

&#x20;   "CS201"

&#x20; ]

}

```



\---



\## Infrastructure Error



```text

connect ECONNREFUSED 127.0.0.1:3000

```



Энэ нь бизнес дүрмийн алдаа биш бөгөөд сервер ажиллахгүй байгаа сүлжээний түвшний алдаа юм.



\---



\# Үр дүнгийн харьцуулалт



| Scenario | Assertions | Failed Assertions | Exit Code |

|----------|----------|----------|----------|

| PASS | 20 | 0 | 0 |

| FAIL | 20 | 1 | 1 |

| DOWN | N/A | Connection Error | 1 |



\---



\# Дүгнэлт



Энэхүү лабораторийн ажлаар REST API системийг Postman болон Newman ашиглан тестэллээ. API-ийн үндсэн бизнес үйлдлүүд болох оюутан үүсгэх, хичээл үүсгэх, хичээлд бүртгүүлэх болон бүртгэлийн жагсаалт авах үйлдлүүдийг шалгасан. Сөрөг тестүүдийн хүрээнд үл мэдэгдэх оюутан, үл мэдэгдэх хичээл болон prerequisite хангагдаагүй нөхцөлүүдийг туршсан. Postman ашиглан request болон response бүрт assertion-ууд үүсгэж шалгасан. Newman ашиглан collection-ийг командын мөрөөс автоматаар ажиллуулсан. PASS ажиллуулалтын үед бүх 20 assertion амжилттай болсон. FAIL ажиллуулалтын үед зориудаар буруу expectation ашиглаж 1 assertion FAIL болгосон. Серверийг унтраасан үед Newman ECONNREFUSED алдааг илрүүлсэн. Бизнес дүрмийн алдаа болон дэд бүтцийн алдааг тусад нь ялгаж шинжилсэн. Лабораторийн ажлын үр дүнд API системийн функциональ болон автомат тестийг Postman ба Newman ашиглан хэрэгжүүлж сурлаа.



\---



\# Хавсаргасан файлууд



```text

server.js



lab05-collection.json

lab05-collection-fail.json



results/

├── newman-pass.txt

├── newman-fail.txt

└── newman-down.txt



