# Data Class

Coming soon...

Okay, so we have created our `FormType` class, used it in our `Controller` process, the
form submit, and we even know how to render it. This is the basic stuff, but it's
already doing a lot for us, but there's one thing that bothers me a little bit and
that's in the controller when we call `$data = $form->getData()` that gives us back in
associative array with all the field data, with all the fields on it. That's super
simple, but it did mean that we needed to do some manual work of creating and setting
that data manually. I'm actually, we don't need to do that in `ArticleFormType`.
There's one other method that we commonly override. Go to the code, generate menu or
command in on a Mac, hit override methods and select `configureOptions()`. Like with
`buildForm()`, we don't need to call the parent method because it's empty inside here
called `$resolver->setDefaults()` pass it an array. This is the way place that you set
options. On this form class, there aren't a lot of options and the main one is
`data_class`, which we're going to set two `Article::class`. What we're doing this binds
that this form to our `Article` class and two cool things are gonna happen.

Okay?

See what this does. Go into your `Controller` and `dd($data)`. All
right, now check this out. Watch closely notice the content, both fields right now or
just text fields because we haven't configured them to be anything else. When we
refresh.

Whoa. The content is now a text area and this is something that we're going to talk
about in a second, but obviously there are ways to configure what types of field,
what type of input. Each field isn't a form. When you bind your form to a class form
system use. It uses something called form type guessing basically because it notice
that the `$content` field on `Article` is a longer text field. It figured that that should
default to a `textarea`. It's just kind of a cool feature. The real important thing
will happen when we submit. Let's read another article called Orion's belt for
fashion or function. Quit create and yes, check it out. It is an `Article` and it has
the `title` and the `content` set on it. This is the power of that `data_class` option.
When this is set on submit, the form system will create a `new Article()` object for us
and then it will use the setter methods to populate the data. So for example, we have
a title per `title` field and any `content` field on our form when we submit the form
actually calls, `setTitle()` and then `setContent()`. It's basically just a convenience for
what we're already doing in our `Controller`. This is awesome because we can now remove
a lot of that duplicated data and instead say `$article = $form->getData()` and to give my an
ide a little bit more help here, I'll give that some inland documentation that says
that this is an `Article`

and that's it. Our controllers now even smaller and when we submit again, it submits
perfectly.

This is the way that we're going to use forms in general by binding them to a class.
However, I want you to remember, if you ever have a very complex field, it's
perfectly okay to not have a `data_class`, get the associative array from your
controller, and then just use that data manually. Also, while you commonly see your
form types bound to an entity class. It doesn't need to be. This `Article` can be any
normal php class. So if you have a form that doesn't look very much like any of your
entities, you could create a new model class that has the exact same properties as
form. Submit that form, get back your model object and the `Controller` and use its
data to populate your other entity objects. Basically, this `data_class` thing is here.
Being able to bind your form to your entity is for convenience, but don't let it be
something that slows you down. All right, while we're here and it's one less thing
out to do, click on create. And now we have our two fields. It's kind of ugly. And
um, and as we know so far, we're not really controlling any of them markup. We're
just calling a few form rendering functions. And then all the markup and all the
fields are being generated automatically

behind the scenes. This is done with something called a form theme. All of the market
being generated on your form comes from somewhere deep inside of Symfony and he can
actually customize that and if you're using bootstrap or maybe foundation, there is a
built informed theme that you can use. Open `config/packages/twig.yaml` and add a
new key called `form_themes` and pointed to a template called `bootstrap_4_layout.html.twig`.
This is actually a template that lives inside of the core of Symfony.
You can hit shift, shift, paste, and find it if you want to. In fact, we'll take a
look at this class later when we talk a little bit more about form themes, but just
by adding this one bit of config can move over. Refresh and yes, our form is now
using bootstrap from the markup, which means it just looks good instantly. That's
awesome. All right. Next, let's talk about customizing the form field types and form
field options so we can make each field look and behave exactly like we want.