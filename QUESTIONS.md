1. What do you mean by @app.route() maps URL to Function?

2. Decorators allows to modify or enhance functions or methods without changing their actual code. What does this mean?

3. Decorator takes the original function, possibly wraps it with additional functionality, and returns a new function. Show a coding example.

4. What is a view function.

5. What does @setupmethod Decorator do in the route() function?

6. What is the difference between Callable and Function?

7. In the below function definition explain what Callable does.


T_route = t.TypeVar("T_route", bound=ft.RouteCallable)

@setupmethod
    def route(self, rule: str, **options: t.Any) -> t.Callable[[T_route], T_route]:
        """Decorate a view function to register it with the given URL
        rule and options. Calls :meth:`add_url_rule`, which has more
        details about the implementation.

        .. code-block:: python

            @app.route("/")
            def index():
                return "Hello, World!"

        See :ref:`url-route-registrations`.

        The endpoint name for the route defaults to the name of the view
        function if the ``endpoint`` parameter isn't passed.

        The ``methods`` parameter defaults to ``["GET"]``. ``HEAD`` and
        ``OPTIONS`` are added automatically.

        :param rule: The URL rule string.
        :param options: Extra options passed to the
            :class:`~werkzeug.routing.Rule` object.
        """

        def decorator(f: T_route) -> T_route:
            endpoint = options.pop("endpoint", None)
            self.add_url_rule(rule, endpoint, f, **options)
            return f

        return decorator


8. What is the use of validate_on_submit() in below function. What validations does it perform?


@app.route('/register', methods=['GET', 'POST'])
def register_page():
    form = RegisterForm()
    if form.validate_on_submit():
        user_to_create = User(username=form.username.data,
                              email_address=form.email_address.data,
                              password=form.password1.data)
        db.session.add(user_to_create)
        db.session.commit()
        return redirect(url_for('market_page'))
    if form.errors != {}: #If there are not errors from the validations
        for err_msg in form.errors.values():
             flash(f'There was an error with creating a user: {err_msg}', category='danger')
    return render_template('register.html', form=form)


*9. What is the type of form variable in register_page() function?


10. The @property decorator transforms a method into a property object, which manages attribute access. Accessing instance.value calls the value method, returning self._value. What do you understand from above statement and below code.

class Example:
    def __init__(self):
        self._value = 0  # Private attribute

    @property
    def value(self):
        """Getter method."""
        return self._value

11. When you define a setter for a property, you're specifying how the attribute should be updated. The setter method must have the same name as the property and is decorated with @<property_name>.setter. What do you understand from above statement and below code.

class Example:
    def __init__(self):
        self._value = 0  # Private attribute

    @property
    def value(self):
        """Getter method."""
        return self._value

    @value.setter
    def value(self, new_value):
        """Setter method with validation."""
        if new_value < 0:
            raise ValueError("Value cannot be negative.")
        self._value = new_value


12. What do you mean by below two statements in the route method?

If the request method is POST, the form binds to the submitted data.
If the request method is GET, the form is unbound and ready to be filled out.


@app.route('/register', methods=['GET', 'POST'])
def register_page():
    form = RegisterForm()
    if form.validate_on_submit():
        user_to_create = User(username=form.username.data,
                              email_address=form.email_address.data,
                              password=form.password1.data)
        db.session.add(user_to_create)
        db.session.commit()
        return redirect(url_for('market_page'))
    if form.errors != {}: #If there are not errors from the validations
        for err_msg in form.errors.values():
             flash(f'There was an error with creating a user: {err_msg}', category='danger')
    return render_template('register.html', form=form)

*13. What is a GET method?

*14. What is a POST method?

15. See the route method and answer the question. Question: User accesses /register via GET; does it execute redirect and render_template?
16. See the route method and answer the question. Question: User submits form via POST and data is valid; does it execute redirect and render_template?
17. See the route method and answer the question. Question: User submits form via POST and data is invalid; does it execute redirect and render_template?

*18. Why do we need to commit after adding?

*19. What is the difference between redirect and render_template?

*20. What is a validation error?

