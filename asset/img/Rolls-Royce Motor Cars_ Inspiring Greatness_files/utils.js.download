/*
 * ADOBE CONFIDENTIAL
 *
 * Copyright 2012 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 *
 */
(function(factory) {
    "use strict";

    if (typeof module === "object" && module.exports) {
        module.exports = factory();
    } else {
        var g = window.Granite = window.Granite || {};
        g.Sling = factory();
    }
}(function() {
    "use strict";

    /**
     * A helper class providing a set of Sling-related utilities.
     * @static
     * @singleton
     * @class Granite.Sling
     * @deprecated Using the constants is no longer needed and actually is not a best practice as it is not RESTful,
     *             where the server should drive the client via hypermedia and the client should not make any
     *             assumption about the URL.
     */
    return {
        /**
         * The selector for infinite hierarchy depth when retrieving repository content.
         * @static
         * @final
         * @type String
         */
        SELECTOR_INFINITY: ".infinity",

        /**
         * The parameter name for the used character set.
         * @static
         * @final
         * @type String
         */
        CHARSET: "_charset_",

        /**
         * The parameter name for the status.
         * @static
         * @final
         * @type String
         */
        STATUS: ":status",

        /**
         * The parameter value for the status type "browser".
         * @static
         * @final
         * @type String
         */
        STATUS_BROWSER: "browser",

        /**
         * The parameter name for the operation.
         * @static
         * @final
         * @type String
         */
        OPERATION: ":operation",

        /**
         * The parameter value for the delete operation.
         * @static
         * @final
         * @type String
         */
        OPERATION_DELETE: "delete",

        /**
         * The parameter value for the move operation.
         * @static
         * @final
         * @type String
         */
        OPERATION_MOVE: "move",

        /**
         * The parameter name suffix for deleting.
         * @static
         * @final
         * @type String
         */
        DELETE_SUFFIX: "@Delete",

        /**
         * The parameter name suffix for setting a type hint.
         * @static
         * @final
         * @type String
         */
        TYPEHINT_SUFFIX: "@TypeHint",

        /**
         * The parameter name suffix for copying.
         * @static
         * @final
         * @type String
         */
        COPY_SUFFIX: "@CopyFrom",

        /**
         * The parameter name suffix for moving.
         * @static
         * @final
         * @type String
         */
        MOVE_SUFFIX: "@MoveFrom",

        /**
         * The parameter name for the ordering.
         * @static
         * @final
         * @type String
         */
        ORDER: ":order",

        /**
         * The parameter name for the replace flag.
         * @static
         * @final
         * @type String
         */
        REPLACE: ":replace",

        /**
         * The parameter name for the destination flag.
         * @static
         * @final
         * @type String
         */
        DESTINATION: ":dest",

        /**
         * The parameter name for the save parameter prefix.
         * @static
         * @final
         * @type String
         */
        SAVE_PARAM_PREFIX: ":saveParamPrefix",

        /**
         * The parameter name for input fields that should be ignored by Sling.
         * @static
         * @final
         * @type String
         */
        IGNORE_PARAM: ":ignore",

        /**
         * The parameter name for login requests.
         * @static
         * @final
         * @type String
         */
        REQUEST_LOGIN_PARAM: "sling:authRequestLogin",

        /**
         * The login URL.
         * @static
         * @final
         * @type String
         */
        LOGIN_URL: "/system/sling/login.html",

        /**
         * The logout URL.
         * @static
         * @final
         * @type String
         */
        LOGOUT_URL: "/system/sling/logout.html"
    };
}));

/*
 * ADOBE CONFIDENTIAL
 *
 * Copyright 2012 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 *
 */
(function(factory) {
    "use strict";

    if (typeof module === "object" && module.exports) {
        module.exports = factory();
    } else {
        var g = window.Granite = window.Granite || {};
        g.Util = factory();
    }
}(function() {
    "use strict";

    // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray#Polyfill
    var isArray = function(arg) {
        return Object.prototype.toString.call(arg) === "[object Array]";
    };

    /**
     * A helper class providing a set of general utilities.
     * @static
     * @singleton
     * @class Granite.Util
     */
    return {
        /**
         * Replaces occurrences of <code>{n}</code> in the specified text with the texts from the snippets.
         *
         * @example
         * var text = Granite.Util.patchText("{0} has signed in.", "Jack");
         * // text = "Jack has signed in."
         * var text2 = Granite.Util.patchText("{0} {1} has signed in from {2}.", ["Jack", "McFarland", "x.x.x.x"]);
         * // text2 = "Jack McFarland has signed in from x.x.x.x."
         *
         * @param {String} text The text.
         * @param {String|String[]} snippets The text(s) replacing <code>{n}</code>.
         * @returns {String} The patched text.
         */
        patchText: function(text, snippets) {
            if (snippets) {
                if (!isArray(snippets)) {
                    text = text.replace("{0}", snippets);
                } else {
                    for (var i = 0; i < snippets.length; i++) {
                        text = text.replace(("{" + i + "}"), snippets[i]);
                    }
                }
            }
            return text;
        },

        /**
         * Returns the top most accessible window.
         * Check {@link .setIFrameMode} to avoid security exception message on WebKit browsers
         * if this method is called in an iFrame included in a window from different domain.
         *
         * @returns {Window} The top window.
         */
        getTopWindow: function() {
            var win = window;
            if (this.iFrameTopWindow) {
                return this.iFrameTopWindow;
            }
            try {
                // try to access parent
                // win.parent.location.href throws an exception if not authorized (e.g. different location in a portlet)
                while (win.parent && win !== win.parent && win.parent.location.href) {
                    win = win.parent;
                }
            } catch (error) {
                // ignored
            }
            return win;
        },

        /**
         * Allows to define if Granite.Util is running in an iFrame and parent window is in another domain
         * (and optionally define what would be the top window in that case.
         * This is necessary to use {@link .getTopWindow} in a iFrame on WebKit based browsers because
         * {@link .getTopWindow} iterates on parent windows to find the top one which triggers a security exception
         * if one parent window is in a different domain. Exception cannot be caught but is not breaking the JS
         * execution.
         *
         * @param {Window} [topWindow=window] The iFrame top window. Must be running on the same host to avoid
         * security exception.
         */
        setIFrameMode: function(topWindow) {
            this.iFrameTopWindow = topWindow || window;
        },

        /**
         * Applies default properties if non-existent into the base object.
         * Child objects are merged recursively.
         * REMARK:
         *   - objects are recursively merged
         *   - simple type object properties are copied over the base
         *   - arrays are cloned and override the base (no value merging)
         *
         * @param {Object} base The object.
         * @param {...Object} pass The objects to be copied onto the base.
         * @returns {Object} The base object with defaults.
         */
        applyDefaults: function() {
            var override;
            var base = arguments[0] || {};

            for (var i = 1; i < arguments.length; i++) {
                override = arguments[i];

                for (var name in override) {
                    var value = override[name];

                    if (override.hasOwnProperty(name) && value !== undefined) {
                        if (value !== null && typeof value === "object" && !(value instanceof Array)) {
                            // nested object
                            base[name] = this.applyDefaults(base[name], value);
                        } else if (value instanceof Array) {
                            // override array
                            base[name] = value.slice(0);
                        } else {
                            // simple type
                            base[name] = value;
                        }
                    }
                }
            }

            return base;
        },

        /**
         * Returns the keycode from the given event.
         * It is a normalized value over variation of browsers' inconsistencies.
         *
         * @param {UIEvent} event The event.
         * @returns {Number} The keycode.
         */
        getKeyCode: function(event) {
            return event.keyCode ? event.keyCode : event.which;
        }
    };
}));

/*
 * ADOBE CONFIDENTIAL
 *
 * Copyright 2012 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 *
 */
/* global CQURLInfo:false, G_XHR_HOOK:false */
/* eslint strict: 0 */
(function(factory) {
    "use strict";

    if (typeof module === "object" && module.exports) {
        module.exports = factory(require("@granite/util"), require("jquery"));
    } else {
        window.Granite.HTTP = factory(Granite.Util, jQuery);
    }
}(function(util, $) {
    /**
     * A helper class providing a set of HTTP-related utilities.
     * @static
     * @singleton
     * @class Granite.HTTP
     */
    return (function() {
        /**
         * The context path used on the server.
         * May only be set by {@link #detectContextPath}.
         * @type String
         */
        var contextPath = null;

        /**
         * The regular expression to detect the context path used
         * on the server using the URL of this script.
         * @readonly
         * @type RegExp
         */
        // eslint-disable-next-line max-len
        var SCRIPT_URL_REGEXP = /^(?:http|https):\/\/[^/]+(\/.*)\/(?:etc\.clientlibs|etc(\/.*)*\/clientlibs|libs(\/.*)*\/clientlibs|apps(\/.*)*\/clientlibs|etc\/designs).*\.js(\?.*)?$/;

        /**
         * The regular expression to match `#` and other non-ASCII characters in a URI.
         * @readonly
         * @type RegExp
         */
        var ENCODE_PATH_REGEXP = /[^\w-.~%:/?[\]@!$&'()*+,;=]/;

        /**
         * The regular expression to parse URI.
         * @readonly
         * @type RegExp
         * @see https://tools.ietf.org/html/rfc3986#appendix-B
         */
        var URI_REGEXP = /^(([^:/?#]+):)?(\/\/([^/?#]*))?([^?#]*)(\?([^#]*))?(#(.*))?/;

        /**
         * Indicates after a session timeout if a refresh has already been triggered
         * in order to avoid multiple alerts.
         * @type String
         */
        var loginRedirected = false;

        var self = {};

        /**
         * Returns the scheme and authority (userinfo, host, port) components of the given URI;
         * or an empty string if the URI does not have the components.
         *
         * This method assumes the URI is valid.
         *
         * e.g. `scheme://userinfo@host:80/path?query#fragment` -> `scheme://userinfo@host:80`
         *
         * @param {String} uri The URI
         * @returns {String} The scheme and authority components
         */
        self.getSchemeAndAuthority = function(uri) {
            if (!uri) {
                return "";
            }

            var result = URI_REGEXP.exec(uri);

            if (result === null) {
                return "";
            }

            return [ result[1], result[3] ].join("");
        };

        /**
         * Returns the context path used on the server.
         *
         * @returns {String} The context path
         */
        self.getContextPath = function() {
            // Keep cache of calculated path.
            if (contextPath === null) {
                contextPath = self.detectContextPath();
            }
            return contextPath;
        };

        /**
         * Detects the context path used on the server.
         *
         * @returns {String} The context path
         * @private
         */
        self.detectContextPath = function() {
            try {
                if (window.CQURLInfo) {
                    contextPath = CQURLInfo.contextPath || "";
                } else {
                    var scripts = document.getElementsByTagName("script");
                    for (var i = 0; i < scripts.length; i++) {
                        var result = SCRIPT_URL_REGEXP.exec(scripts[i].src);
                        if (result) {
                            contextPath = result[1];
                            return contextPath;
                        }
                    }
                    contextPath = "";
                }
            } catch (e) {
                // ignored
            }

            return contextPath;
        };

        /**
         * Makes sure the specified relative URL starts with the context path
         * used on the server. If an absolute URL is passed, it will be returned
         * as-is.
         *
         * @param {String} url The URL
         * @returns {String} The externalized URL
         */
        self.externalize = function(url) {
            try {
                if (url.indexOf("/") === 0 && self.getContextPath() && url.indexOf(self.getContextPath() + "/") !== 0) {
                    url = self.getContextPath() + url;
                }
            } catch (e) {
                // ignored
            }
            return url;
        };

        /**
         * Removes scheme, authority and context path from the specified
         * absolute URL if it has the same scheme and authority as the
         * specified document (or the current one). If a relative URL is passed,
         * the context path will be stripped if present.
         *
         * @param {String} url The URL
         * @param {String} doc (optional) The document
         * @returns {String} The internalized URL
         */
        self.internalize = function(url, doc) {
            if (url.charAt(0) === "/") {
                if (contextPath === url) {
                    return "";
                } else if (contextPath && url.indexOf(contextPath + "/") === 0) {
                    return url.substring(contextPath.length);
                } else {
                    return url;
                }
            }

            if (!doc) {
                doc = document;
            }
            var docHost = self.getSchemeAndAuthority(doc.location.href);
            var urlHost = self.getSchemeAndAuthority(url);
            if (docHost === urlHost) {
                return url.substring(urlHost.length + (contextPath ? contextPath.length : 0));
            } else {
                return url;
            }
        };

        /**
         * Removes all parts but the path from the specified URL.
         * <p>Examples:<pre><code>
         /x/y.sel.html?param=abc => /x/y
         </code></pre>
         * <pre><code>
         http://www.day.com/foo/bar.html => /foo/bar
         </code></pre><p>
         *
         * @param {String} url The URL, may be empty. If empty <code>window.location.href</code> is taken.
         * @returns {String} The path
         */
        self.getPath = function(url) {
            if (!url) {
                if (window.CQURLInfo && CQURLInfo.requestPath) {
                    return CQURLInfo.requestPath;
                } else {
                    url = window.location.pathname;
                }
            } else {
                url = self.removeParameters(url);
                url = self.removeAnchor(url);
            }

            url = self.internalize(url);
            var i = url.indexOf(".", url.lastIndexOf("/"));
            if (i !== -1) {
                url = url.substring(0, i);
            }
            return url;
        };

        /**
         * Removes the fragment component from the given URI.
         *
         * This method assumes the URI is valid.
         *
         * e.g. `scheme://userinfo@host:80/path?query#fragment` -> `scheme://userinfo@host:80/path?query`
         *
         * @param {String} uri The URI
         * @returns {String} The URI without fragment component
         */
        self.removeAnchor = function(uri) {
            var fragmentIndex = uri.indexOf("#");
            if (fragmentIndex >= 0) {
                return uri.substring(0, fragmentIndex);
            } else {
                return uri;
            }
        };

        /**
         * Removes the query component and its subsequent fragment component from the given URI.
         * i.e. When query component exists, the subsequent fragment component is also removed.
         * However, when query component doesn't exist, fragment component is not removed.
         *
         * The assumption here is that the usages of `#` before the `?` are intended as part of the path component
         * that need to be encoded separately.
         * This assumption is made because `c.d.cq.commons.jcr.JcrUtil#isValidName` allows `#`.
         *
         * e.g. `scheme://userinfo@host:80/path#with#hash?query#fragment` -> `scheme://userinfo@host:80/path#with#hash`
         *
         * @param {String} uri The URL
         * @returns {String} The URI without the query component and its subsequent fragment component
         */
        self.removeParameters = function(uri) {
            var queryIndex = uri.indexOf("?");
            if (queryIndex >= 0) {
                return uri.substring(0, queryIndex);
            } else {
                return uri;
            }
        };

        /**
         * Encodes the path component of the given URI if it is not already encoded.
         * See {@link #encodePath} for the details of the encoding.
         *
         * e.g. `scheme://userinfo@host:80/path#with#hash?query#fragment`
         * -> `scheme://userinfo@host:80/path%23with%23hash?query#fragment`
         *
         * @param {String} uri The URI to encode
         * @returns {String} The encoded URI
         */
        self.encodePathOfURI = function(uri) {
            var DELIMS = [ "?", "#" ];

            var parts = [ uri ];
            var delim;
            for (var i = 0, ln = DELIMS.length; i < ln; i++) {
                delim = DELIMS[i];
                if (uri.indexOf(delim) >= 0) {
                    parts = uri.split(delim);
                    break;
                }
            }

            if (ENCODE_PATH_REGEXP.test(parts[0])) {
                parts[0] = self.encodePath(parts[0]);
            }

            return parts.join(delim);
        };

        /**
         * Encodes the given URI using `encodeURI`.
         *
         * This method is used to encode URI components from the scheme component up to the path component (inclusive).
         * Therefore, `?` and `#` are also encoded in addition.
         *
         * However `[` and `]` are not encoded.
         * The assumption here is that the usages of `[` and `]` are only at the host component (for IPv6),
         * not at the path component.
         * This assumption is made because `c.d.cq.commons.jcr.JcrUtil#isValidName` disallows `[` and `]`.
         *
         * Examples
         *
         * * `scheme://userinfo@host:80/path?query#fragment` -> `scheme://userinfo@host:80/path%3Fquery%23fragment`
         * * `http://[2001:db8:85a3:8d3:1319:8a2e:370:7348]/` -> `http://[2001:db8:85a3:8d3:1319:8a2e:370:7348]/`
         *
         * @param {String} uri The URI to encode
         * @returns {String} The encoded URI
         */
        self.encodePath = function(uri) {
            uri = encodeURI(uri);

            // Decode back `%5B` and `%5D`.
            // The `[` and `]` are not valid characters at the path component and need to be encoded,
            // which `encodeURI` does correctly.
            // However as mentioned in the doc, they are assumed to be used for authority component only.
            uri = uri.replace(/%5B/g, "[").replace(/%5D/g, "]");

            uri = uri.replace(/\?/g, "%3F");
            uri = uri.replace(/#/g, "%23");

            return uri;
        };

        /**
         * Handles login redirection if needed.
         */
        self.handleLoginRedirect = function() {
            if (!loginRedirected) {
                loginRedirected = true;
                alert(Granite.I18n.get("Your request could not be completed because you have been signed out."));

                var l = util.getTopWindow().document.location;
                l.href = self.externalize("/") + "?resource=" + encodeURIComponent(l.pathname + l.search + l.hash);
            }
        };

        /**
         * Gets the XHR hooked URL if called in a portlet context
         *
         * @param {String} url The URL to get
         * @param {String} method The method to use to retrieve the XHR hooked URL
         * @param {Object} params The parameters
         * @returns {String} The XHR hooked URL if available, the provided URL otherwise
         */
        self.getXhrHook = function(url, method, params) {
            method = method || "GET";
            if (window.G_XHR_HOOK && typeof G_XHR_HOOK === "function") {
                var p = {
                    "url": url,
                    "method": method
                };
                if (params) {
                    p["params"] = params;
                }
                return G_XHR_HOOK(p);
            }
            return null;
        };

        /**
         * Evaluates and returns the body of the specified response object.
         * Alternatively, a URL can be specified, in which case it will be
         * requested using a synchronous {@link #get} in order to acquire
         * the response object.
         *
         * @param {Object|String} response The response object or URL
         * @returns {Object} The evaluated response body
         * @since 5.3
         */
        self.eval = function(response) {
            if (typeof response !== "object") {
                response = $.ajax({
                    url: response,
                    type: "get",
                    async: false
                });
            }
            try {
                // support responseText for backward compatibility (pre 5.3)
                var text = response.body ? response.body : response.responseText;
                return JSON.parse(text);
            } catch (e) {
                // ignored
            }
            return null;
        };

        return self;
    }());
}));

/*
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2012 Adobe
 * All Rights Reserved.
 *
 * NOTICE: All information contained herein is, and remains
 * the property of Adobe and its suppliers, if any. The intellectual
 * and technical concepts contained herein are proprietary to Adobe
 * and its suppliers and are protected by all applicable intellectual
 * property laws, including trade secret and copyright laws.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe.
 */
(function(factory) {
    "use strict";

    if (typeof module === "object" && module.exports) {
        module.exports = factory(require("@granite/http"));
    } else {
        window.Granite.I18n = factory(window.Granite.HTTP);
    }
}(function(HTTP) {
    "use strict";

    /**
     * A helper class providing a set of utilities related to internationalization (i18n).
     *
     * <h3>Locale Priorities</h3>
     * <p>The locale is read based on the following priorities:</p>
     * <ol>
     *   <li>manually specified locale</li>
     *   <li><code>document.documentElement.lang</code></li>
     *   <li><code>Granite.I18n.LOCALE_DEFAULT</code></li>
     * </ol>
     *
     * <h3>Dictionary Priorities</h3>
     * <p>The dictionary URL is read based on the following priorities:</p>
     * <ol>
     *   <li>manually specified URL (<code>urlPrefix</code, <code>urlSuffix</code>)</li>
     *   <li><code>data-i18n-dictionary-src</code> attribute at &lt;html&gt; element,
     *       which has the type of <a href="http://tools.ietf.org/html/rfc6570">URI Template</a> string</li>
     *   <li>The URL resolved from default <code>urlPrefix</code> and <code>urlSuffix</code></li>
     * </ol>
     *
     * <h3>URI Template of data-i18n-dictionary-src</h3>
     * <p>It expects the variable named <code>locale</code>,
     * which will be fetched from the locale (based on priorities above).
     * E.g. <code>&lt;html lang="en" data-i18n-dictionary-src="/libs/cq/i18n/dict.{+locale}.json"&gt;</code>.</p>
     *
     * @static
     * @class Granite.I18n
     */
    return (function() {
        /**
         * The map where the dictionaries are stored under their locale.
         * @type Object
         */
        var dicts = {};

        /**
         * The prefix for the URL used to request dictionaries from the server.
         * @type String
         */
        var urlPrefix = "/libs/cq/i18n/dict.";

        /**
         * The suffix for the URL used to request dictionaries from the server.
         * @type String
         */
        var urlSuffix = ".json";

        /**
         * The manually specified locale as a String or a function that returns the locale as a string.
         * @type String
         */
        var manualLocale = undefined;

        /**
         * If the current locale represents pseudo translations.
         * In that case the dictionary is expected to provide just a special
         * translation pattern to automatically convert all original strings.
         */
        var pseudoTranslations = false;

        var languages = null;

        var self = {};

        /**
         * Indicates if the dictionary parameters are specified manually.
         */
        var manualDictionary = false;

        var getDictionaryUrl = function(locale) {
            if (manualDictionary) {
                return urlPrefix + locale + urlSuffix;
            }

            var dictionarySrc;
            var htmlEl = document.querySelector("html");
            if (htmlEl) {
                dictionarySrc = htmlEl.getAttribute("data-i18n-dictionary-src");
            }

            if (!dictionarySrc) {
                return urlPrefix + locale + urlSuffix;
            }

            // dictionarySrc is a URITemplate
            // Use simple string replacement for now; for more complicated scenario, please use Granite.URITemplate
            return dictionarySrc.replace("{locale}", encodeURIComponent(locale)).replace("{+locale}", locale);
        };

        var patchText = function(text, snippets) {
            if (snippets) {
                if (Array.isArray(snippets)) {
                    for (var i = 0; i < snippets.length; i++) {
                        text = text.replace("{" + i + "}", snippets[i]);
                    }
                } else {
                    text = text.replace("{0}", snippets);
                }
            }
            return text;
        };

        /**
         * The default locale (en).
         * @readonly
         * @type String
         */
        self.LOCALE_DEFAULT = "en";

        /**
         * The language code for pseudo translations.
         * @readonly
         * @type String
         */
        self.PSEUDO_LANGUAGE = "zz";

        /**
         * The dictionary key for pseudo translation pattern.
         * @readonly
         * @type String
         */
        self.PSEUDO_PATTERN_KEY = "_pseudoPattern_";

        /**
         * Initializes I18n with the given config options:
         * <ul>
         * <li>locale: the current locale (defaults to "en")</li>
         * <li>urlPrefix: the prefix for the URL used to request dictionaries from
         * the server (defaults to "/libs/cq/i18n/dict.")</li>
         * <li>urlSuffix: the suffix for the URL used to request dictionaries from
         * the server (defaults to ".json")</li>
         * </ul>
         * Sample config. The dictionary would be requested from
         * "/apps/i18n/dict.fr.json":
         <code><pre>{
         "locale": "fr",
         "urlPrefix": "/apps/i18n/dict.",
         "urlSuffix": ".json"
         }</pre></code>
         *
         * @param {Object} config The config
         */
        self.init = function(config) {
            config = config || {};

            this.setLocale(config.locale);
            this.setUrlPrefix(config.urlPrefix);
            this.setUrlSuffix(config.urlSuffix);
        };

        /**
         * Sets the current locale.
         *
         * @param {String|Function} locale The locale or a function that returns the locale as a string
         */
        self.setLocale = function(locale) {
            if (!locale) {
                return;
            }
            manualLocale = locale;
        };

        /**
         * Returns the current locale based on the priorities.
         *
         * @returns {String} The locale
         */
        self.getLocale = function() {
            if (typeof manualLocale === "function") {
                // execute function first time only and store result in currentLocale
                manualLocale = manualLocale();
            }
            return manualLocale || document.documentElement.lang || self.LOCALE_DEFAULT;
        };

        /**
         * Sets the prefix for the URL used to request dictionaries from
         * the server. The locale and URL suffix will be appended.
         *
         * @param {String} prefix The URL prefix
         */
        self.setUrlPrefix = function(prefix) {
            if (!prefix) {
                return;
            }
            urlPrefix = prefix;
            manualDictionary = true;
        };

        /**
         * Sets the suffix for the URL used to request dictionaries from
         * the server. It will be appended to the URL prefix and locale.
         *
         * @param {String} suffix The URL suffix
         */
        self.setUrlSuffix = function(suffix) {
            if (!suffix) {
                return;
            }
            urlSuffix = suffix;
            manualDictionary = true;
        };

        /**
         * Returns the dictionary for the specified locale. This method
         * will request the dictionary using the URL prefix, the locale,
         * and the URL suffix. If no locale is specified, the current
         * locale is used.
         *
         * @param {String} locale (optional) The locale
         * @returns {Object} The dictionary
         */
        self.getDictionary = function(locale) {
            locale = locale || self.getLocale();

            if (!dicts[locale]) {
                pseudoTranslations = locale.indexOf(self.PSEUDO_LANGUAGE) === 0;

                try {
                    var xhr = new XMLHttpRequest();
                    xhr.open("GET", HTTP.externalize(getDictionaryUrl(locale)), false);
                    xhr.send();

                    dicts[locale] = JSON.parse(xhr.responseText);
                } catch (e) {
                    // ignored
                }
                if (!dicts[locale]) {
                    dicts[locale] = {};
                }
            }
            return dicts[locale];
        };

        /**
         * Translates the specified text into the current language.
         *
         * @param {String} text The text to translate
         * @param {String[]} snippets The snippets replacing <code>{n}</code> (optional)
         * @param {String} note A hint for translators (optional)
         * @returns {String} The translated text
         */
        self.get = function(text, snippets, note) {
            var dict;
            var newText;
            var lookupText;

            dict = self.getDictionary();

            // note that pseudoTranslations is initialized in the getDictionary() call above
            lookupText = pseudoTranslations ? self.PSEUDO_PATTERN_KEY
                : note ? text + " ((" + note + "))"
                    : text;
            if (dict) {
                newText = dict[lookupText];
            }
            if (!newText) {
                newText = text;
            }
            if (pseudoTranslations) {
                newText = newText.replace("{string}", text).replace("{comment}", note ? note : "");
            }
            return patchText(newText, snippets);
        };

        /**
         * Translates the specified text into the current language. Use this
         * method to translate String variables, e.g. data from the server.
         *
         * @param {String} text The text to translate
         * @param {String} note A hint for translators (optional)
         * @returns {String} The translated text
         */
        self.getVar = function(text, note) {
            if (!text) {
                return null;
            }
            return self.get(text, null, note);
        };

        /**
         * Returns the available languages, including a "title" property with a display name:
         * for instance "German" for "de" or "German (Switzerland)" for "de_ch".
         *
         * @returns {Object} An object with language codes as keys and an object with "title",
         *                  "language", "country" and "defaultCountry" members.
         */
        self.getLanguages = function() {
            if (!languages) {
                try {
                    // use overlay servlet so customers can define /apps/wcm/core/resources/languages
                    // TODO: broken!!!
                    var url = HTTP.externalize("/libs/wcm/core/resources/languages.overlay.infinity.json");
                    var xhr = new XMLHttpRequest();
                    xhr.open("GET", url, false);
                    xhr.send();

                    var json = JSON.parse(xhr.responseText);

                    Object.keys(json).forEach(function(prop) {
                        var lang = json[prop];
                        if (lang.language) {
                            lang.title = self.getVar(lang.language);
                        }
                        if (lang.title && lang.country && lang.country !== "*") {
                            lang.title += " (" + self.getVar(lang.country) + ")";
                        }
                    });
                    languages = json;
                } catch (e) {
                    languages = {};
                }
            }
            return languages;
        };

        /**
         * Parses a language code string such as "de_CH" and returns an object with
         * language and country extracted. The delimiter can be "_" or "-".
         *
         * @param {String} langCode a language code such as "de" or "de_CH" or "de-ch"
         * @returns {Object} an object with "code" ("de_CH"), "language" ("de") and "country" ("CH")
         *                  (or null if langCode was null)
         */
        self.parseLocale = function(langCode) {
            if (!langCode) {
                return null;
            }
            var pos = langCode.indexOf("_");
            if (pos < 0) {
                pos = langCode.indexOf("-");
            }

            var language;
            var country;
            if (pos < 0) {
                language = langCode;
                country = null;
            } else {
                language = langCode.substring(0, pos);
                country = langCode.substring(pos + 1);
            }
            return {
                code: langCode,
                language: language,
                country: country
            };
        };

        return self;
    }());
}));

/*
 * ADOBE CONFIDENTIAL
 *
 * Copyright 2012 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 *
 */
(function(factory) {
    "use strict";

    if (typeof module === "object" && module.exports) {
        module.exports = factory();
    } else {
        var g = window.Granite = window.Granite || {};
        g.TouchIndicator = factory();
    }
}(function() {
    "use strict";

    function createIndicator() {
        var el = document.createElement("div");
        el.style.visibility = "hidden";
        // fixed would be better, but flickers on ipad while scrolling
        el.style.position = "absolute";
        el.style.width = "30px";
        el.style.height = "30px";
        el.style.borderRadius = "20px";
        el.style.border = "5px solid orange";
        el.style.userSelect = "none";
        el.style.opacity = "0.5";
        el.style.zIndex = "2000";
        el.style.pointerEvents = "none";
        return el;
    }

    var used = {};

    var unused = [];

    /**
     * Implements the "Adobe Dynamic Touch Indicator" that tracks touch events and displays a visual indicator for
     * screen sharing and presentation purposes.
     *
     * To enable it, call <code>Granite.TouchIndicator.init()</code> e.g. on document ready:
     * <pre><code>
     * Granite.$(document).ready(function() {
     *     Granite.TouchIndicator.init();
     * });
     * </code></pre>
     *
     * AdobePatentID="2631US01"
     */
    return {
        debugWithMouse: false,

        init: function() {
            var self = this;

            var update = function(e) {
                self.update(e.touches);
                return true;
            };
            document.addEventListener("touchstart", update);
            document.addEventListener("touchmove", update);
            document.addEventListener("touchend", update);

            if (this.debugWithMouse) {
                document.addEventListener("mousemove", function(e) {
                    e.identifer = "fake";
                    self.update([ e ]);
                    return true;
                });
            }
        },

        update: function(touches) {
            // go over all touch events present in the array
            var retained = {};
            for (var i = 0; i < touches.length; i++) {
                var touch = touches[i];
                var id = touch.identifier;

                // check if we already have a indicator with the correct id
                var indicator = used[id];
                if (!indicator) {
                    // if not, check if we have an unused one
                    indicator = unused.pop();

                    // if not, create a new one and append it to the dom
                    if (!indicator) {
                        indicator = createIndicator();
                        document.body.appendChild(indicator);
                    }
                }

                retained[id] = indicator;
                indicator.style.left = (touch.pageX - 20) + "px";
                indicator.style.top = (touch.pageY - 20) + "px";
                indicator.style.visibility = "visible";
            }

            // now hide all unused ones and stuff them in the unused array
            for (id in used) {
                if (used.hasOwnProperty(id) && !retained[id]) {
                    indicator = used[id];
                    indicator.style.visibility = "hidden";
                    unused.push(indicator);
                }
            }
            used = retained;
        }
    };
}));

/*
 * ADOBE CONFIDENTIAL
 *
 * Copyright 2012 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 *
 */
(function(factory) {
    "use strict";

    if (typeof module === "object" && module.exports) {
        module.exports = factory();
    } else {
        var g = window.Granite = window.Granite || {};
        g.OptOutUtil = factory();
    }
}(function($) {
    "use strict";

    function trim(s) {
        if (String.prototype.trim) {
            return s.trim();
        }
        return s.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, "");
    }

    /**
     * A library to determine whether any opt-out cookie is set and whether a given cookie name is white-listed.
     *
     * The opt-out and white-list cookie names are determined by a server-side configuration
     * (<code>com.adobe.granite.security.commons.OptOutService</code>) and provided to this tool by an optionally
     * included component (<code>/libs/granite/security/components/optout</code>) which provides a global JSON object
     * named <code>GraniteOptOutConfig</code>.
     *
     * @static
     * @class Granite.OptOutUtil
     */
    return (function() {
        var self = {};

        /**
         * The names of cookies the presence of which indicates the user has opted out.
         * @type String[]
         */
        var optOutCookieNames = [];

        /**
         * The names of cookies which may still be set in spite of the user having opted out.
         * @type String[]
         */
        var whitelistedCookieNames = [];

        /**
         * Initializes this tool with an opt-out configuration.
         *
         * The following options are supported:
         * <ul>
         *     <li>cookieNames: an array of cookie names representing opt-out cookies. Defaults to empty.</li>
         *     <li>whitelistCookieNames: an array of cookies representing white-listed cookies. Defaults to empty.</li>
         * </ul>
         *
         * @param {Object} config The opt-out configuration.
         *
         * @example
         * {
         *     "cookieNames": ["omniture_optout","cq-opt-out"],
         *     "whitelistCookieNames": ["someAppCookie", "anotherImportantAppCookie"]
         * }
         */
        self.init = function(config) {
            if (config) {
                optOutCookieNames = config.cookieNames || [];
                whitelistedCookieNames = config.whitelistCookieNames || [];
            } else {
                optOutCookieNames = [];
                whitelistedCookieNames = [];
            }
        };

        /**
         * Returns the array of configured cookie names representing opt-out cookies.
         *
         * @returns {String[]} The cookie names.
         */
        self.getCookieNames = function() {
            return optOutCookieNames;
        };

        /**
         * Returns the array of configured cookie names representing white-listed cookies.
         *
         * @returns {String[]} The cookie names.
         */
        self.getWhitelistCookieNames = function() {
            return whitelistedCookieNames;
        };

        /**
         * Determines whether the user (browser) has elected to opt-out.
         * This is indicated by the presence of one of the cookies retrieved through {@link #getCookieNames()}.
         *
         * @returns {Boolean} <code>true</code> if an opt-cookie was found in the browser's cookies;
         *     <code>false</code> otherwise.
         */
        self.isOptedOut = function() {
            var browserCookies = document.cookie.split(";");
            for (var i = 0; i < browserCookies.length; i++) {
                var cookie = browserCookies[i];
                var cookieName = trim(cookie.split("=")[0]);
                if (self.getCookieNames().indexOf(cookieName) >= 0) {
                    return true;
                }
            }
            return false;
        };

        /**
         * Determines whether the given <code>cookieName</code> may be used to set a cookie.
         * This is the case if either opt-out is inactive (<code>{@link #isOptedOut()} === false</code>) or it is
         * active and the give cookie name was found in the white-list ({@link #getWhitelistCookieNames()}).
         *
         * @param {String} cookieName The name of the cookie to check.
         * @returns {Boolean} <code>true</code> if a cookie of this name may be used with respect to the opt-out status;
         *     <code>false</code> otherwise.
         */
        self.maySetCookie = function(cookieName) {
            return !(self.isOptedOut() && self.getWhitelistCookieNames().indexOf(cookieName) === -1);
        };

        return self;
    }());
}));

/*
 * ADOBE CONFIDENTIAL
 *
 * Copyright 2012 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 *
 */


//------------------------------------------------------------------------------
// Initialize the Granite utils library

Granite.OptOutUtil.init(window.GraniteOptOutConfig);
Granite.HTTP.detectContextPath();

