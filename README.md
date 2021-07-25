# Postman

ДЗ Postman
=====

=====

1) необходимо залогиниться
POST
http://116.203.27.46:5002/login
login : str (кроме /)
password : str

Приходящий токен необходимо передать во все остальные запросы.

===================
дальше все запросы требуют наличие токена.
===================

http://116.203.27.46:5002/user_info
req.
POST
age: int
salary: int
name: str
auth_token


resp.
{'start_qa_salary':salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
                                'u_age':age,
                                'u_salary_1.5_year': salary * 4}
                                }

Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
===================

http://116.203.27.46:5002/new_data
req.
POST
age: int
salary: int
name: str
auth_token

Resp.
{'name':name,
  'age': int(age),
  'salary': [salary, str(salary*2), str(salary*3)]}

Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://116.203.27.46:5002 (http://188.130.138.105:5001/new_data)/get_test_user
4) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
5) проверить, что 2-й элемент массива salary больше 1-го и 0-го
===================

http://116.203.27.46:5002/test_pet_info
req.
POST
age: int
weight: int
name: str
auth_token


Resp.
{'name': name,
 'age': age,
 'daily_food':weight * 0.012,
 'daily_sleep': weight * 2.5}


Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент.

===================

http://116.203.27.46:5002/get_test_user
req.
POST
age: int
salary: int
name: str
auth_token

Resp.
{'name': name,
 'age':age,
 'salary': salary,
 'family':{'children':[['Alex', 24],['Kate', 12]],
 'u_salary_1.5_year': salary * 4}
  }

Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) Проверить что занчение поля name = значению переменной name из окружения
4) Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age

===================

http://116.203.27.46:5002/currency
req.
POST
auth_token

Resp. Передаётся список массив объектов.
[
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
…
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
]

Тесты:
1) Можете взять любой объект из присланного списка, используйте js random.
В объекте возьмите Cur_ID и передать через окружение в следующий запрос.

 ===================

http://116.203.27.46:5002/curr_byn
req.
POST
auth_token
curr_code: int

Resp.
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}

Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.


===============
***
1) получить список валют
2) итерировать список валют
3) в каждой итерации отправлять запрос на сервер для получения курса каждой валюты
4) если возвращается 500 код, переходим к следующей итреации
5) если получаем 200 код, проверяем response json на наличие поля "Cur_OfficialRate"
6) если поле есть, пишем в консоль инфу про фалюту в виде response
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}
7) переходим к следующей итерации
-----------------------------------------------------------------------------------------------------

Task 2. Postman, GIT.

Postman.

endpoint_1: object_info_1
method: GET
request_params: 
   1) age (int)
   2) weight (int)
   3) name (str)

response: 
{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}
========

endpoint_2: object_info_2
method: GET
request_params: 
   1) age (int)
   2) salary (int)
   3) name (str)

response: 
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }

=========

endpoint_3: object_info_3
method: GET
request_params: 
   1) age (int)
   2) salary (int)
   3) name (str)

response: 
result = {'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'pets': {'cat':{'name':'Sunny',
                                     'age': 3},
                              'dog':{'name':'Luky',
                                     'age': 4}},
                     'u_salary_1_5_year': salary * 4}
          }

=========

endpoint_4: object_info_4
method: GET
request_params: 
   1) age (int)
   2) name (str)
   3) salary (int)

response: 
result = {'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2), str(salary * 3)]}

============================

endpoint_5: user_info_1
method: POST
form_params: 
   1) age (int)
   2) weight (int)
   3) name (str)

response: 
{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}
========

endpoint_6: user_info_2
method: POST
form_params: 
   1) age (int)
   2) salary (int)
   3) name (str)

response: 
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }

=========

endpoint_7: user_info_3
method: POST
form_params: 
   1) age (int)
   2) salary (int)
   3) name (str)

response: 
result = {'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'u_salary_1_5_year': salary * 4}
          }

=========

endpoint_8: user_info_4
method: POST
form_params: 
   1) age (int)
   2) name (str)
   3) salary (int)

response: 
result = {'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2.5), str(salary * 3.5)]}






Задание.
1) Выполнить в Postman endpoints 1,2,7,8.
2) Сделать репозиторий в Гит
3) Склонировать репозиторий на локальный компьютер.
4) Експортировать тесты endpoints 1,2,7,8 и окружение в папку git склонированного репозитория.
5) Запушить тесты на внешний репозиторий
6) Сделать в GIT отдельную ветку.
7) Сделать тесты ендроинтов 3, 6 в Postman
8) Кспортировать тесты в новую, созданную ветку GIT.
9) Запушить новую ветку на внешний репозиторий. Тесты должны появиться на внешнем репозитории созданной в ветке
10) Вмержить изменения новой ветки в основную.
11) Запушить изменения основной ветки на внешний репозиторий.
12) Сделать в GIT отдельную ветку.
13) Сделать тесты ендроинтов 4,5 в Postman
14) Экспортировать тесты в созданную ветку GIT.
15) Запушить новую ветку на внешний репозиторий. Тесты должны появиться на внешнем репозитории созданной в ветке.
16) Вмержить изменения ветки в основную ветку.
17) Запушить изменения основной ветки на внешний репозиторий.



-----------------------------------------------------------------------------------------------------
Task Charles.
 
Protocol: http
IP: 162.55.220.72
Port: 5005

EP_1
Method: GET
EndPoint: /get_method
request url params: 
 name: str
 age: int

response: 
[
    “Str”,
    “Str”
]

Task:
Подменить url в Charles чтобы в запросе ушло имя которые вы вписали в Postman, а вернулось то, которое вы подставили в Charles.

==================

EP_2
Method: POST
EndPoint: /user_info_3
request form data: 
 name: str
 age: int
 salary: int

response: 
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'u_salary_1_5_year': salary * 4}}

Task:
Подменить body в Charles так чтобы в запросе ушла salary которую вы вписали в Postman, а в u_salary_1_5_year цифра вернулась меньше оригинальной из запроса.

==================

EP_3
Method: GET
EndPoint: /object_info_1
request url params: 
 name: str
 age: int
 weight: int

response: 
{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}

Task:
Подменить параметры запроса в Charles так, чтобы в Postman пришел ответ где другое name, daily_food > weight из запроса, а daily_sleep < weight из запроса.

==================

EP_4
Method: GET
EndPoint: /object_info_3
request url params: 
 name: str
 age: int
 salary: int

response: 
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'pets': {'cat':{'name':'Sunny',
                                     'age': 3},
                              'dog':{'name':'Luky',
                                     'age': 4}},
                     'u_salary_1_5_year': salary * 4}
          }

Task:
Сделать через Charles так, чтобы сервер вернул 500 ошибку.

==================

EP_5
Method: GET
EndPoint: /object_info_4
request url params: 
 name: str
 age: int
 salary: int

response: 
{'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2), str(salary * 3)]}


Task:
Сделать через Charles так, чтобы сервер вернул 405 ошибку.

==================

EP_6
Method: POST
EndPoint: /user_info_2
request form data: 
 name: str
 age: int
 salary: int

response: 
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }


Task:
Сделать через Charles так, чтобы в Postman вернулся ответ, в котором qa_salary_after_1.5_year переименовано в qa_salary_after_1.5_month
