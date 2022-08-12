---
layout: post
title: "Django Many to Many Relationship"
tags: ["django", "orm"]
---

# Many to Many for form in both classes

```python
class ManyToManyField_NoSyncdb(models.ManyToManyField):
    def __init__(self, *args, **kwargs):
        super(ManyToManyField_NoSyncdb, self).__init__(*args, **kwargs)
        self.creates_table = False

class User(models.Model):
    groups = ManyToManyField('Group', related_name='groups', db_table=u'USERS_TO_GROUPS')
class Group(models.Model):
    users = ManyToManyField_NoSyncdb(User, related_name='users', db_table=u'USERS_TO_GROUPS')

# ManyToManyField.symmetrical : only on self
class Person(models.Model):
  friends = models.ManyToManyField("self") # I am your friend, then you are my friend.
  friends = models.ManyToManyField("self", symmetrical=False) # the oposite
```

* ManyToManyField.through : to relate additional data

```python
class Contact(models.Model):
    contacts = models.ManyToManyField('self', through='ContactRelationship', symmetrical=False,)

class ContactRelationship(models.Model):
    types = models.ManyToManyField('RelationshipType',related_name='contact_relationships',blank=True)
    from_contact = models.ForeignKey('Contact', related_name='from_contacts')
    to_contact = models.ForeignKey('Contact', related_name='to_contacts')

    class Meta:
        unique_together = ('from_contact', 'to_contact')
```

For simetrical self, add related_name='related_contacts+', to Contact

```python
crm.ContactRelationship.objects.create(from_contact=contact_a, to_contact=contact_b)
crm.ContactRelationship.objects.create(from_contact=contact_b, to_contact=contact_a)
```
