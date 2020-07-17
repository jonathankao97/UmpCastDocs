# Leagues App Serializers

All serializers are displayed in expanded (repr) view

## League Private Serializer

Used for Create, Retrieve, Update, Destroy operations. Displays all information about league (hence, private). Includes division and role serializers nested inside.
No extra validations.

        LeaguePrivateSerializer():
          pk = IntegerField(label='ID', read_only=True)
          title = CharField(max_length=64)
          description = CharField(allow_blank=True, allow_null=True, max_length=1028, required=False, style={'base_template': 'textarea.html'})
          divisions = DivisionSerializer(many=True, read_only=True, source='division_set'):
            pk = IntegerField(label='ID', read_only=True)
            title = CharField(max_length=64)
            league = PrimaryKeyRelatedField(read_only=True)
            ts_id = IntegerField(max_value=2147483647, min_value=-2147483648, required=False)
            roles = RoleSerializer(many=True, read_only=True, source='role_set'):
                pk = IntegerField(label='ID', read_only=True)
                title = CharField(max_length=64)
                division = PrimaryKeyRelatedField(read_only=True)
          league_picture = ImageField(allow_null=True, max_length=100, required=False)
          public_access = BooleanField(required=False)
          date_joined = DateTimeField(read_only=True)
          expiration_date = DateTimeField(required=False)
          adv_scheduling_limit = IntegerField(max_value=2147483647, min_value=-2147483648, required=False)
          ts_id = IntegerField(max_value=2147483647, min_value=-2147483648, required=False)
          opponent_library = JSONField(encoder=None, required=False, style={'base_template': 'textarea.html'})

## League Public Serializer

Used for List and Filter operations. Displays only public information. Fields cannot be edited.
No extra validations.

        LeaguePublicSerializer():
            pk = IntegerField(label='ID', read_only=True)
            title = CharField(read_only=True)
            description = CharField(read_only=True, style={'base_template': 'textarea.html'})
            league_picture = ImageField(read_only=True)

## Division Serializer

Used for all Division Operations. Displays all information about a division, including nested roles.

Extra Validation: can only attach a division to a league that you own

        DivisionSerializer():
            pk = IntegerField(label='ID', read_only=True)
            title = CharField(max_length=64)
            league = PrimaryKeyRelatedField(read_only=True)
            ts_id = IntegerField(max_value=2147483647, min_value=-2147483648, required=False)
            roles = RoleSerializer(many=True, read_only=True, source='role_set'):
                pk = IntegerField(label='ID', read_only=True)
                title = CharField(max_length=64)
                division = PrimaryKeyRelatedField(read_only=True)

## Role Serializer

Used for all Role Operations. Displays all information about a role

Extra Validation: can only attach a role to a division that is attached to a league that you own

        RoleSerializer():
            pk = IntegerField(label='ID', read_only=True)
            title = CharField(max_length=64)
            division = PrimaryKeyRelatedField(read_only=True)
