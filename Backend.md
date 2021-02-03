## Получение вопросов ##

__URL:__ https://employment-assistant.onti.actcognitive.org/api/questionnaries/get_questionnary

__Методы:__ get

__Аргументы:__ questionnary_name

__Доступные опросы:__ [test_questionnary](https://employment-assistant.onti.actcognitive.org/api/questionnaries/get_questionnary?questionnary_name=test_questionnary), [omo](https://employment-assistant.onti.actcognitive.org/api/questionnaries/get_questionnary?questionnary_name=omo), [zaslon](https://employment-assistant.onti.actcognitive.org/api/questionnaries/get_questionnary?questionnary_name=zaslon)

## Отправка ответов ##

__URL:__ https://employment-assistant.onti.actcognitive.org/api/questionnaries/dump_qustionnary_answers

__Методы:__ post

__Данные для отправки:__

```
	{
	    "questionnary_name": "test_questionnary",
	    "answers": {
	        "1": "10",
	        "2": "3",
	        "3": "5",
	        "4": "1",
	        "5": "2",
	        "6": "8"
	    }
	}
```

