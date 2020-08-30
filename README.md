# simple-saas
- This django project is meant to serve as a boilerplate code for building any saas tool

- The directory `saas` serves as a django app with all the boilerplate code

- django-rest-framework is used for authentication and creating apis. Please refer to [this](https://github.com/encode/django-rest-framework)
 if not familiar with django-rest-framework since this project heavily relies on it.

- business logic for all APIs is present in serializers.

- to use this as a library, refer to [this](https://github.com/rzrokon/Django-SaaS#using-as-a-library)

#### Signup
```curl
curl -XPOST 'http://localhost:8000/saas/signup' -d '{"business": {"name": "test inc"}, "email": "test@test.com", "first_name": "sankalp", "last_name": "jonna", "password1": "pleasepass", "password2": "pleasepass"}' -H "Content-type: application/json"
```

#### Login
```curl
curl -XPOST 'http://localhost:8000/saas/login' -d '{"email": "test@test.com", "password": "pleasepass"}' -H "Content-type: application/json"
```

#### Reset password
```curl
curl -XPOST 'http://localhost:8000/saas/passwd/reset' -d '{"email": "test@test.com"}' -H "Content-type: application/json"
```

#### Reset password confirmation
```curl
curl -XPOST 'http://localhost:8000/saas/passwd/reset/cnfrm' -d '{"activation_key": "<activation_key>", "password1": "sankalp", "password2": "sankalp"}' -H "Content-type: application/json"
```

#### Me
```curl
curl -XGET 'http://localhost:8000/saas/me' -H "Authorization: Token <token>"
```

#### Invite
```curl
curl -XPOST 'http://localhost:8000/saas/invite' -H "Authorization: Token 534fe89f5d6b9ff214e8883d7b9664177002056a" -H "Content-Type: application/json" -d '{"email": "test5@test.com"}'
```

#### Prefill Signup form
```curl
curl -XGET 'http://localhost:8000/saas/signup/prefill?key=<activation_key>'
```

### Using as a library
If you feel that the current functionality is enough and you wish to simply use the `saas` app in your existing django project, follow these steps

#### Installation
```sh
pip install git+https://github.com/rzrokon/Django-SaaS
```

#### add saas and rest_framework to INSTALLED_APPS
```python
INSTALLED_APPS = [
	'saas',

	'rest_framework.authtoken',
	'rest_framework',
]
```

#### add rest_framework settings
```python
REST_FRAMEWORK = {
	'DEFAULT_AUTHENTICATION_CLASSES': (
		'rest_framework.authentication.TokenAuthentication',
	),
}
```

#### run migrations
```sh
python manage.py migrate
```

#### add to urls.py
in the root urls, add
```python
urlpatterns = [
	url(r'^', include('django.contrib.auth.urls')),
	url(r'^admin/', admin.site.urls),
    url(r'^saas/', include('saas.urls')),
]
```
