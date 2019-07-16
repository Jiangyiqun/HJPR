# Backend API Documentation

@base: http://localhost:5000

## Get the cloud

- URL: @base/api/cloud
- Method: GET
- Content: Null

### Success Response

Return the list of skills in all courses, and the number of courses for each skill.

- CODE: 200
- Content:

```json
{
    "analysis": 0.01,
    "modern geometric": 0.005,
    "python": 0.02
}
```

## Get the skills

- URL: @base/api/skills
- Method: GET
- Content: Null

### Success Response

Return the list of skills in all courses.

- CODE: 200
- Content:

```json
{
    "skills": [ "Python", "analysis", "modern geometric"]
}
```

## Get the courses

- URL: @base/api/courses
- Method: GET
- Content: Null

### Success Response

return the list of all courses

- CODE: 200
- Content:

```json
{
    "courses": [ "TSMA2004", "TSMA4100", "AUT2201"]
}
```

## Get the suggested courses

- URL: @base/api/suggest
- Method: POST
- Content:
  
```json
{
    "skills": [ "analysis", "python", "problem solving"],
    "courses": [ "TSMA2004", "TSMA4100", "AUT2201"],
    "questions": [],
}
```

### Success Response

return a list of recommended courses sorted according to the relevance in descending order

- CODE: 200
- Content:

```json
{
    "courses": [
        {
            "label": "MA3402",
            "value": 0.7,
            "desc": "desc"
        },
        {
            "label": "MUSP4145",
            "value": 0.2,
            "desc": "desc"
        }
    ]
}
```

### Error Response

return an error message if the client has sent bad request

- CODE: 400
- Content:

```json
{
    "errorMsg": "whatever error messeage specified by backend"
}
```

### Interface of suggest function

```python
import suggest from ./rakegenism/runner.py as rakegenism

parameter = {
    "skills": [ "analysis", "python", "problem solving"],
    "courses": [ "TSMA2004", "TSMA4100", "AUT2201"],
    "questions": [],
}

code, value = rakegenism(parameter)

if succeed:
    code = 0
    value = {
    "courses": [
        {
            "label": "MA3402",
            "value": 0.7,
            "desc": "desc"
        },
        {
            "label": "MUSP4145",
            "value": 0.2,
            "desc": "desc"
        }
        ]
    }
else:
    code = 1
    value = "Error"
```

## Get course information

- URL: @base/api/course/@course_code
- Method: GET
- Content: Null

### Success Response

return the skills and similar courses which should be sorted in descending order

- CODE: 200
- Content:

```json

{
    "courseCode": "course code",
    "skills": [ "analysis", "python", "problem solving"],
    "courseDesc": "course description",
    "similarCourses" :["TSMA2004", "TSMA4100", "AUT2201"],
    "courseUrl": "http://the home page of that course"

}
```

### Error Response

return when the course code does not exist

- CODE: 404
- Content:

```json
{   
    "courseCode": "course code",
    "errorMsg": "the course code does not exist"
}
```


## References

- [Course Website](https://webcms3.cse.unsw.edu.au/COMP9900/19T2/)
- [Google Drive](https://drive.google.com/drive/folders/17uxR4HrlkMTmWBHJNuZqe2dFg7krcCz2?usp=sharing)
- [Trello](https://trello.com/b/An48d5C7/hjpr)