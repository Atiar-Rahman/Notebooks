




```python

from django.db import models
from apps.core.models import BaseModel
# Create your models here.

class Banner(BaseModel):
    title = models.CharField(max_length=200)
    subtitle = models.TextField(blank=True, null=True)
    image = models.ImageField(upload_to='banner/')
    button_text = models.CharField(max_length=100, blank=True)
    button_link = models.URLField(blank=True)
    order = models.PositiveIntegerField(default=0)
    
    class Meta:
        ordering = ['order']
        
    def __str__(self):
        return self.title
    
    
    
class FooterInfo(BaseModel):
    logo = models.ImageField(
        upload_to="footer/",
        blank=True,
        null=True
    )

    company_name = models.CharField(
        max_length=200
    )

    description = models.TextField(
        blank=True,
        null=True
    )

    address = models.TextField(
        blank=True,
        null=True
    )

    phone = models.CharField(
        max_length=20,
        blank=True,
        null=True
    )

    email = models.EmailField(
        blank=True,
        null=True
    )

    copyright_text = models.CharField(
        max_length=255,
        blank=True,
        null=True
    )


    class Meta:
        verbose_name = "Footer Information"
        verbose_name_plural = "Footer Information"


    def __str__(self):
        return self.company_name
    
    
class FooterSocialLink(BaseModel):

    PLATFORM_CHOICES = (
        ("facebook", "Facebook"),
        ("youtube", "Youtube"),
        ("instagram", "Instagram"),
        ("linkedin", "LinkedIn"),
        ("twitter", "Twitter"),
        ("github", "Github"),
    )

    platform = models.CharField(
        max_length=50,
        choices=PLATFORM_CHOICES
    )

    url = models.URLField()

    icon = models.CharField(
        max_length=100,
        blank=True,
        null=True,
        help_text="Example: fa-facebook"
    )

    order = models.PositiveIntegerField(
        default=0
    )


    class Meta:
        ordering = ["order"]
        verbose_name = "Footer Social Link"
        verbose_name_plural = "Footer Social Links"


    def __str__(self):
        return self.platform
    

# Footer Menu Section
class FooterMenu(BaseModel):

    title = models.CharField(
        max_length=100
    )

    order = models.PositiveIntegerField(
        default=0
    )

    class Meta:
        ordering = ["order"]

    def __str__(self):
        return self.title



# Footer Menu Items
class FooterMenuItem(BaseModel):

    menu = models.ForeignKey(
        FooterMenu,
        on_delete=models.CASCADE,
        related_name="items"
    )

    name = models.CharField(
        max_length=100
    )

    url = models.CharField(
        max_length=255
    )

    order = models.PositiveIntegerField(
        default=0
    )

    class Meta:
        ordering = ["order"]

    def __str__(self):
        return self.name



# Useful Links
class UsefulLink(BaseModel):

    title = models.CharField(
        max_length=100
    )

    url = models.CharField(
        max_length=255
    )

    order = models.PositiveIntegerField(
        default=0
    )

    class Meta:
        ordering = ["order"]

    def __str__(self):
        return self.title



# Quick Links
class QuickLink(BaseModel):

    title = models.CharField(
        max_length=100
    )

    url = models.CharField(
        max_length=255
    )

    order = models.PositiveIntegerField(
        default=0
    )

    class Meta:
        ordering = ["order"]

    def __str__(self):
        return self.title



# Payment Gateway Logo
class PaymentGatewayLogo(BaseModel):

    name = models.CharField(
        max_length=100
    )

    logo = models.ImageField(
        upload_to="payment_gateway/"
    )

    website = models.URLField(
        blank=True,
        null=True
    )

    order = models.PositiveIntegerField(
        default=0
    )

    class Meta:
        ordering = ["order"]

    def __str__(self):
        return self.name



# Mobile App Download Link
class AppDownloadLink(BaseModel):

    APP_CHOICES = (
        ("android", "Android"),
        ("ios", "iOS"),
    )

    platform = models.CharField(
        max_length=20,
        choices=APP_CHOICES
    )

    store_name = models.CharField(
        max_length=100
    )

    icon = models.ImageField(
        upload_to="app_download/",
        blank=True,
        null=True
    )

    url = models.URLField()

    order = models.PositiveIntegerField(
        default=0
    )

    class Meta:
        ordering = ["order"]

    def __str__(self):
        return self.store_name
```

