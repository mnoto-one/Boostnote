---
title: 2 - forms modelForm
tags:
  - Django
  - Forms
  - ModelForm
---

### 📜 List files
```python
1 -> "website/views.py"
2 -> "website/forms.py"
3 -> "contact-us.html"
```
---

### 💬 Forms
 📁 -1 website/forms.py
```python
from django.forms import ModelForm, Textarea, EmailInput, TextInput
from .models import ContactUs


class ContactForm(ModelForm):
    class Meta:
        model = ContactUs
        fields = ['full_name', 'addess_email', 'number_mobile', 'subject', 'message']
        widgets = {
            'full_name': TextInput(attrs={"class": "form-control", "placeholder": "نام خود را وارد کنید *"}),
            'addess_email': EmailInput(attrs={"class": "form-control", "placeholder": "ایمیل خود را وارد کنید *"}),
            'number_mobile': TextInput(attrs={"class": "form-control", "placeholder": "شماره موبایل خود را وارد کنید"}),
            'subject': TextInput(attrs={"class": "form-control", "placeholder": "موضوع پیام شما"}),
            'message': Textarea(attrs={"class": "form-control", "placeholder": "متن پیام شما *"}),
        }

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Views
 📁 -2 website/views.py
```python
from django.contrib import messages
from . import forms
...
def contactus_view(request):
    contact_form = forms.ContactForm(request.POST or None)
    context = {
        "form": contact_form
    }

    if contact_form.is_valid():
        messages.success(request, 'ارسال شد')
        print(context["form"].save())

    return render(request, 'website/pages/contact-us.html', context)
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Html
 📁 -3 contact-us.html
```html
<form method="post" class="contact-form mb-3">
    {% csrf_token %}
    <div class="row">
        <div class="col-sm-12">
            {{ form.non_field_errors }}
        </div>
        <div class="col-sm-6">
            <label for="cname" class="sr-only">نام</label>
            {{ form.full_name }}
            {{ form.full_name.errors }}
        </div><!-- End .col-sm-6 -->

        <div class="col-sm-6">
            <label for="cemail" class="sr-only">ایمیل</label>
            {{ form.addess_email }}
            {{ form.addess_email.errors }}
        </div><!-- End .col-sm-6 -->
    </div><!-- End .row -->

    ...

    
    <button type="submit" class="btn btn-outline-primary-2 btn-minwidth-sm float-right">
        <span>تایید و ارسال</span>
        <i class="icon-long-arrow-left"></i>
    </button>
</form>
```
