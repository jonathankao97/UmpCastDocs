# Users App Serializers

## User Profile Private Serializer

Used for Create, Retrieve, and Update operations. Displays all information about User (hence, private).

        UserProfilePrivateSerializer():
            pk = IntegerField(label='ID', read_only=True)
            account_type = ChoiceField(choices=(('umpire', 'umpire'), ('manager', 'manager'), ('inactive', 'inactive')), required=False)
            leagues = PrimaryKeyRelatedField(many=True, queryset=League.objects.all(), required=False)
            email = EmailField(max_length=255, validators=[<UniqueValidator(queryset=User.objects.all())>])
            email_notifications = BooleanField(required=False)
            first_name = CharField(max_length=255)
            last_name = CharField(max_length=255)
            is_configured = BooleanField(required=False)
            phone_number = CharField(allow_blank=True, max_length=10, required=False)
            phone_notifications = BooleanField(required=False)
            profile_picture = ImageField(allow_null=True, max_length=100, required=False)
            date_joined = DateTimeField(required=False)
            password = CharField(max_length=128, write_only=True)
            password2 = CharField(max_length=128, write_only=True)


Extra Validations:
- Password validated using django built in password validator
- Password2 validated against password for equality
- Phone number must be of length 10 and only contain numeric values
- Create: First_name, Last_name, email, password, and password2 must all be specified


## User Profile Public Serializer

Used for list and filter operations. Displays only public information about user. This info cannot be edited. No extra validations

        UserProfilePublicSerializer():
          pk = IntegerField(label='ID', read_only=True)
          first_name = CharField(read_only=True)
          last_name = CharField(read_only=True)
          profile_picture = ImageField(read_only=True)
          date_joined = DateTimeField(read_only=True)
          account_type = ChoiceField(choices=(('umpire', 'umpire'), ('manager', 'manager'), ('inactive', 'inactive')), read_only=True)
