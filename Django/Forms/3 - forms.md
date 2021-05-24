---
title: 3 - forms
tags:
  - Django
  - Forms
---

### 💬 Overriding the default fields

```python
from django.forms import ModelForm, Textarea
from myapp.models import Author

class AuthorForm(ModelForm):
    class Meta:
        model = Author
        fields = ('name', 'title', 'birth_date')
        widgets = {
            'name': Textarea(attrs={'cols': 80, 'rows': 20}),
        }

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Rendering fields manually
```html
{{ form.non_field_errors }}
<div class="fieldWrapper">
    {{ form.subject.errors }}
    <label for="{{ form.subject.id_for_label }}">Email subject:</label>
    {{ form.subject }}
</div>
<div class="fieldWrapper">
    {{ form.message.errors }}
    <label for="{{ form.message.id_for_label }}">Your message:</label>
    {{ form.message }}
</div>
<div class="fieldWrapper">
    {{ form.sender.errors }}
    <label for="{{ form.sender.id_for_label }}">Your email address:</label>
    {{ form.sender }}
</div>
<div class="fieldWrapper">
    {{ form.cc_myself.errors }}
    <label for="{{ form.cc_myself.id_for_label }}">CC yourself?</label>
    {{ form.cc_myself }}
</div>
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Looping over the form’s fields
```html
{% for field in form %}
    <div class="fieldWrapper">
        {{ field.errors }}
        {{ field.label_tag }} {{ field }}
        {% if field.help_text %}
        <p class="help">{{ field.help_text|safe }}</p>
        {% endif %}
    </div>
{% endfor %}
```

#### 💬 Useful attributes on {{ field }} include:

* 📌 {{ field.label }}
```
The label of the field, e.g. Email address.
```

* 📌 {{ field.label_tag }}
```
The field’s label wrapped in the appropriate HTML <label> tag.
This includes the form’s label_suffix. For example, the default label_suffix is a colon:
```

```html
<label for="id_email">Email address:</label>
```
* 📌 {{ field.id_for_label }}
```
The ID that will be used for this field (id_email in the example above).
If you are constructing the label manually, you may want to use this in lieu of label_tag.
It’s also useful, for example, if you have some inline JavaScript and want to avoid hardcoding the field’s ID.
```

* 📌 {{ field.value }}
```
The value of the field. e.g someone@example.com.
```


* 📌 {{ field.html_name }}
```
The name of the field that will be used in the input element’s name field. This takes the form prefix into account, if it has been set.
```

* 📌 {{ field.html_name }}
```
The name of the field that will be used in the input element’s name field. This takes the form prefix into account, if it has been set.
```
* 📌 {{ field.help_text }}

```
Any help text that has been associated with the field.
```
* 📌 {{ field.errors }}

```
Outputs a <ul class="errorlist"> containing any validation errors corresponding to this field.
You can customize the presentation of the errors with a {% for error in field.errors %} loop.
In this case, each object in the loop is a string containing the error message.
```
* 📌 {{ field.is_hidden }}

```
This attribute is True if the form field is a hidden field and False otherwise.
It’s not particularly useful as a template variable, but could be useful in conditional tests such as:
```
```html
{% if field.is_hidden %}
   {# Do something special #}
{% endif %}
```

* 📌 {{ field.field }}

```
The Field instance from the form class that this BoundField wraps.
You can use it to access Field attributes, e.g. {{ char_field.field.max_length }}.
```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
