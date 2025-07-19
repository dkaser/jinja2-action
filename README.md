Jinja2 is a fast and straightforward templating engine. You can use this action
to easily run it in your GitHub workflows.

# Using input variables

```yml
- name: Setup nginx
  uses: dkaser/jinja2-action@v1.3.0
  with:
    template: infra/nginx.conf.j2
    output_file: infra/nginx.conf
    strict: true
    variables: |
      server_host=staging.example.com
      timeout=30s
```

# Using data files

```yml
- name: Setup nginx
  uses: dkaser/jinja2-action@v1.3.0
  with:
    template: infra/nginx.conf.j2
    output_file: infra/nginx.conf
    data_file: staging_config.json
    data_format: json # Will try to guess from the extension instead (unnecessary in this case)
```

# Using environment variables

```yml
- name: Setup nginx
  uses: dkaser/jinja2-action@v1.3.0
  with:
    template: infra/nginx.conf.j2
    output_file: infra/nginx.conf
  env:
    SERVER_HOST: staging.example.com
```

Environment variables are used this way in the template file:

```
{{ env['SERVER_HOST'] }} <-- This is always strict
```

```
{{ env.get('SERVER_HOST') }} <-- This is never strict, and displays `None` if you don't specify a default value
```

# See also

- [Jinja2 docs](https://jinja.palletsprojects.com/)

# License

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License.

You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
