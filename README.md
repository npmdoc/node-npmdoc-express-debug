# api documentation for  [express-debug (v1.1.1)](https://github.com/devoidfury/express-debug)  [![npm package](https://img.shields.io/npm/v/npmdoc-express-debug.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-express-debug) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-express-debug.svg)](https://travis-ci.org/npmdoc/node-npmdoc-express-debug)
#### debug toolbar middleware for developing applications in expressjs

[![NPM](https://nodei.co/npm/express-debug.png?downloads=true)](https://www.npmjs.com/package/express-debug)

[![apidoc](https://npmdoc.github.io/node-npmdoc-express-debug/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-express-debug_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-express-debug/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-express-debug/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-express-debug/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Tom Hunkapiller"
    },
    "bugs": {
        "url": "https://github.com/devoidfury/express-debug/issues"
    },
    "dependencies": {
        "connectr": "0.0.6",
        "jade": "0.29.0",
        "xtend": "2.0.3"
    },
    "description": "debug toolbar middleware for developing applications in expressjs",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "8eabe378b3d96b74172c8f2df817d342161057b6",
        "tarball": "https://registry.npmjs.org/express-debug/-/express-debug-1.1.1.tgz"
    },
    "homepage": "https://github.com/devoidfury/express-debug",
    "keywords": [
        "express",
        "debug",
        "tool",
        "development",
        "toolbar"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "devoidfury",
            "email": "tom@mostlyserious.io"
        }
    ],
    "name": "express-debug",
    "optionalDependencies": {},
    "peerDependencies": {
        "express": ">= 3.0.0 < 5"
    },
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/devoidfury/express-debug.git"
    },
    "scripts": {},
    "version": "1.1.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module express-debug](#apidoc.module.express-debug)
1.  object <span class="apidocSignatureSpan">express-debug.</span>request
1.  object <span class="apidocSignatureSpan">express-debug.</span>response
1.  object <span class="apidocSignatureSpan">express-debug.</span>utils

#### [module express-debug.request](#apidoc.module.express-debug.request)
1.  [function <span class="apidocSignatureSpan">express-debug.request.</span>add (req, args)](#apidoc.element.express-debug.request.add)
1.  [function <span class="apidocSignatureSpan">express-debug.request.</span>clear (index)](#apidoc.element.express-debug.request.clear)
1.  [function <span class="apidocSignatureSpan">express-debug.request.</span>list (index)](#apidoc.element.express-debug.request.list)
1.  [function <span class="apidocSignatureSpan">express-debug.request.</span>rawBody (req, res, next)](#apidoc.element.express-debug.request.rawBody)

#### [module express-debug.response](#apidoc.module.express-debug.response)
1.  [function <span class="apidocSignatureSpan">express-debug.response.</span>init (app, settings)](#apidoc.element.express-debug.response.init)

#### [module express-debug.utils](#apidoc.module.express-debug.utils)
1.  [function <span class="apidocSignatureSpan">express-debug.utils.</span>flatten (arr, out)](#apidoc.element.express-debug.utils.flatten)
1.  [function <span class="apidocSignatureSpan">express-debug.utils.</span>get_ms_from_ns (ns)](#apidoc.element.express-debug.utils.get_ms_from_ns)
1.  [function <span class="apidocSignatureSpan">express-debug.utils.</span>inject_toolbar (str, toolbar)](#apidoc.element.express-debug.utils.inject_toolbar)



# <a name="apidoc.module.express-debug"></a>[module express-debug](#apidoc.module.express-debug)



# <a name="apidoc.module.express-debug.request"></a>[module express-debug.request](#apidoc.module.express-debug.request)

#### <a name="apidoc.element.express-debug.request.add"></a>[function <span class="apidocSignatureSpan">express-debug.request.</span>add (req, args)](#apidoc.element.express-debug.request.add)
- description and source-code
```javascript
add = function (req, args) {
    panels.finalize(req);

    if (panels.use_requests) {
        var data = {
            body:        Object.keys(req.body).length ? req.body : req.rawBody,
            query:       Object.keys(req.query).length ? req.query : undefined,
            method:      req.method,
            path:        req.path,
            locals:      req.res.locals,
            send_args:   args,
            req_headers: req.headers,
            res_headers: req.res._headers,
            panels:      req.EDT
        };
        // break any references
        requests.push(JSON.parse(JSON.stringify(data)));
        data = null;
    }
}
```
- example usage
```shell
...
        // inject toolbar callback into render callback
        res._EDT_orig_render.call(res, view, options, toolbar_callback);
    }
};

var send = function() {
    if (this.EDT_rendered !== true) {
        request.add(this.req, arguments);
    }
    this._EDT_orig_send.apply(this, arguments);
};

response.patch = function(res) {
    res._EDT_orig_render = res.render;
    res.render = render;
...
```

#### <a name="apidoc.element.express-debug.request.clear"></a>[function <span class="apidocSignatureSpan">express-debug.request.</span>clear (index)](#apidoc.element.express-debug.request.clear)
- description and source-code
```javascript
clear = function (index) {
    requests = requests.slice(index, requests.length)
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.express-debug.request.list"></a>[function <span class="apidocSignatureSpan">express-debug.request.</span>list (index)](#apidoc.element.express-debug.request.list)
- description and source-code
```javascript
list = function (index) {
    index = index || 0;

    return requests.slice(index, requests.length);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.express-debug.request.rawBody"></a>[function <span class="apidocSignatureSpan">express-debug.request.</span>rawBody (req, res, next)](#apidoc.element.express-debug.request.rawBody)
- description and source-code
```javascript
rawBody = function (req, res, next) {
    var data = '';
    req.setEncoding('utf8');
    req.on('data', function (chunk) { data += chunk; });
    req.on('end', function () { req.rawBody = data || undefined; });
    next();
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.express-debug.response"></a>[module express-debug.response](#apidoc.module.express-debug.response)

#### <a name="apidoc.element.express-debug.response.init"></a>[function <span class="apidocSignatureSpan">express-debug.response.</span>init (app, settings)](#apidoc.element.express-debug.response.init)
- description and source-code
```javascript
init = function (app, settings) {
    var theme = null;

    // user-supplied css
    if (settings.theme) {
        try {
            theme = fs.readFileSync(settings.theme, 'utf-8');
        } catch (e) {
            console.error('EDT: error loading css file at ' + settings.theme);
            console.error('please check that the path is correct. Err: ', e);
        }
    }

    // replaces res.render and injects express-debug toolbar
    var render = function (view, options, fn) {
        options = options || {};

        var res = this,
            req = this.req,
            app = this.app,
            accept = req.headers.accept || '';


        var finalize = function (err, str) {
            // keep existing callback if one was passed
            if (typeof fn === 'function') {
                fn(err, str);
            } else if (err) {
                req.next(err);
            } else {
                res.send(str);
            }
        };

        panels.finalize(req);

        // support callback function as second arg
        if (typeof options === 'function') {
            fn = options;
            options = {};
        }

        // merge res.locals
        options._locals = res.locals;

        var render_toolbar = function (str, callback) {
            var standalone = settings.path === req.path;
            var opts = {
                EDTsettings: settings,
                theme:       theme,
                req:         req,
                standalone:  standalone,
                extra_attrs: settings.extra_attrs,
                panels:      panels.render({
                    locals: options,
                    app:    app,
                    res:    res,
                    req:    req,
                    view:   view
                }, settings, standalone)
            };

            jade.renderFile(template, opts, function (err, toolbar) {
                callback(err, err ? undefined : utils.inject_toolbar(str, toolbar));
            });
        };

        var toolbar_callback = function (err, str) {
            panels.post_render(req);

            if (err) {
                console.log(err);
                req.next(err);

                // skip if this client req isn't expecting html or is ajax
            } else if (accept.indexOf('html') === -1 ||  req.xhr) {
                res.send(str);

            } else if (res.EDT_rendered) {
                // if callback method was used, more than one template may be rendered.
                // in this care, do not render another copy
                // TODO: see if we can catch this on the last render, and attach it in .send instead
                finalize(err, str);

            } else {
                res.EDT_rendered = true;
                render_toolbar(str, finalize);
            }
        };

        panels.pre_render(req);
        if (req.path.indexOf(settings.path) === 0) {
            // standalone mode
            jade.renderFile(fullpage, function (err, str) {
                toolbar_callback(err, str);
            });

        } else {
            // inject toolbar callback into render callback
            res._EDT_orig_render.call(res, view, options, toolbar_callback);
        }
    };

    var send = function() {
        if (this.EDT_rendered !== true) {
            request.add(this.req, arguments);
        }
        this._EDT_orig_send.apply(this, arguments);
    };

    response.patch = function(res) {
        res._EDT_orig_render = res.render;
        res.render = render;
        res._EDT_orig_send = res.send;
        res.send = send;
    }
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.express-debug.utils"></a>[module express-debug.utils](#apidoc.module.express-debug.utils)

#### <a name="apidoc.element.express-debug.utils.flatten"></a>[function <span class="apidocSignatureSpan">express-debug.utils.</span>flatten (arr, out)](#apidoc.element.express-debug.utils.flatten)
- description and source-code
```javascript
flatten = function (arr, out) {
    out = out || [];

    if (arr instanceof Array) {
        arr.forEach(function (item, i) {
            if (item instanceof Array) {
                utils.flatten(item, out);
            } else {
                item.EDT_parent = item.EDT_parent || arr;
                item.EDT_index = i;
                out.push(item)
            }
        });
    }

    return out;
}
```
- example usage
```shell
...
    // flatten a multidimensional array, with references
    flatten: function(arr, out) {
out = out || [];

if (arr instanceof Array) {
    arr.forEach(function (item, i) {
        if (item instanceof Array) {
            utils.flatten(item, out);
        } else {
            item.EDT_parent = item.EDT_parent || arr;
            item.EDT_index = i;
            out.push(item)
        }
    });
}
...
```

#### <a name="apidoc.element.express-debug.utils.get_ms_from_ns"></a>[function <span class="apidocSignatureSpan">express-debug.utils.</span>get_ms_from_ns (ns)](#apidoc.element.express-debug.utils.get_ms_from_ns)
- description and source-code
```javascript
get_ms_from_ns = function (ns) {
    return (ns / 10000 | 0) / 100;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.express-debug.utils.inject_toolbar"></a>[function <span class="apidocSignatureSpan">express-debug.utils.</span>inject_toolbar (str, toolbar)](#apidoc.element.express-debug.utils.inject_toolbar)
- description and source-code
```javascript
inject_toolbar = function (str, toolbar) {
    var location = str.lastIndexOf('</body');

    if (location === -1) {
        location = str.lastIndexOf('</html');
    }

    if (location === -1) {
        str += toolbar;
    } else {
        str = str.substring(0, location) + toolbar + str.substring(location);
    }
    return str;
}
```
- example usage
```shell
...
        res:    res,
        req:    req,
        view:   view
    }, settings, standalone)
};

jade.renderFile(template, opts, function (err, toolbar) {
    callback(err, err ? undefined : utils.inject_toolbar(str, toolbar));
});
        };

        var toolbar_callback = function (err, str) {
panels.post_render(req);

if (err) {
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
