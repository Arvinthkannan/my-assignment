
from django.db import models
from django.db.models.signals import post_save
from django.dispatch import receiver
import time
@receiver(post_save, sender=models.Model)
def my_signal_handler(sender, instance, created, **kwargs):
    print("Signal started")
    time.sleep(2)  
    print("Signal completed")
class MyModel(models.Model):
    name = models.CharField(max_length=100)
from django.http import HttpResponse
from .models import MyModel
def trigger_signal(request):
    print("Before saving the model")
    MyModel.objects.create(name="Test")
    print("After saving the model")
    return HttpResponse("Signal triggered!")
