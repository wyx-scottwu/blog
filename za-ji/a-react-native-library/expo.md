# Expo

{% code title=".env" %}
```properties
# expo environment variabels
# 官方解释⬇️
# We use `WEB_PUBLIC_URL` environment variable or "homepage" field to infer
# "public path" at which the app is served.
# Webpack needs to know it to put the right <script> hrefs into HTML even in
# single-page apps that may serve index.html for nested URLs like /todos/42.
# We can't use a relative path in HTML because we don't want to load something
# like /todos/42/static/js/bundle.7289d.js. We have to know the root.
WEB_PUBLIC_URL=XXX
```
{% endcode %}
