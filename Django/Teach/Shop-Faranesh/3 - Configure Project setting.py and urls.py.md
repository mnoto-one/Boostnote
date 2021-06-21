---
title: 3 - Configure Project setting.py and urls.py
tags:
  - Django
  - Faranesh
  - Configure
---

### 📜 List files
```python
1 -> "django_project/settings.py"
2 -> "django_project/urls.py"
```
---


### 💬 INSTALLED_APPS
📁 -1 django_project/settings.py
```python
...

# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'website.apps.WebsiteConfig',
    'shop.apps.ShopConfig',
    'cart.apps.CartConfig',
    'zeep',
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',
]

...

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                ...
                'cart.context_processor.cart'
            ],
        },
    },
]

...

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/3.2/howto/static-files/

STATIC_URL = '/static/'
# STATIC_ROOT = BASE_DIR / 'static'
STATICFILES_DIRS = [BASE_DIR / 'static']
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
CART_SESSION_ID = 'cart'
LOGIN_REDIRECT_URL = 'shop:index'

AUTHENTICATION_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
)
SITE_ID = 1
SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'APP': {
            'client_id': '238510566263-ccta82d7kes7b8hdbs97m6s4nis1smob.apps.googleusercontent.com',
            'secret': 'aArON6dwp_e_7oz_ITtidfk6',
            'key': ''
        }
    }
}
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_HOST_USER = '*****************'
EMAIL_HOST_PASSWORD = '***********************'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
# Default primary key field type
# https://docs.djangoproject.com/en/3.2/ref/settings/#default-auto-field

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Urls
📁 -1 django_project/urls.py

```python
from django.contrib import admin
from django.urls import path,include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('shop.urls')),
    path('cart/', include('cart.urls')),
    path('accounts/', include('allauth.urls'))

]
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```
