# Projects

The following libraries and projects are known to work with babashka.

- [Projects](#projects)
  - [Libraries](#libraries)
    - [clj-http-lite](#clj-http-lite)
    - [spartan.spec](#spartanspec)
    - [missing.test.assertions](#missingtestassertions)
    - [medley](#medley)
    - [limit-break](#limit-break)
    - [clojure-csv](#clojure-csv)
    - [regal](#regal)
    - [cprop](#cprop)
    - [comb](#comb)
    - [nubank/docopt](#nubankdocopt)
    - [arrangement](#arrangement)
    - [clojure.math.combinatorics](#clojuremathcombinatorics)
    - [testdoc](#testdoc)
    - [doric](#doric)
    - [clojure.data.zip](#clojuredatazip)
    - [clj-psql](#clj-psql)
    - [camel-snake-kebab](#camel-snake-kebab)
    - [aero](#aero)
    - [clojure.data.generators](#clojuredatagenerators)
    - [honeysql](#honeysql)
    - [bond](#bond)
    - [portal](#portal)
    - [version-clj](#version-clj)
    - [matchete](#matchete)
    - [progrock](#progrock)
    - [clj-commons/fs](#clj-commonsfs)
    - [cljc.java-time](#cljcjava-time)
    - [environ](#environ)
    - [gaka](#gaka)
    - [failjure](#failjure)
    - [pretty](#pretty)
    - [clojure-term-colors](#clojure-term-colors)
    - [binf](#binf)
    - [rewrite-edn](#rewrite-edn)
    - [expound](#expound)
    - [omniconf](#omniconf)
  - [Pods](#pods)
  - [Projects](#projects-1)
    - [babashka-test-action](#babashka-test-action)
    - [deps.clj](#depsclj)
    - [4bb](#4bb)
    - [babashka lambda layer](#babashka-lambda-layer)
    - [Release on push Github action](#release-on-push-github-action)
    - [justone/bb-scripts](#justonebb-scripts)
    - [nativity](#nativity)
    - [cldwalker/bb-clis](#cldwalkerbb-clis)
    - [krell template](#krell-template)
    - [wee-httpd](#wee-httpd)
    - [covid19-babashka](#covid19-babashka)
    - [bb-spotify](#bb-spotify)
    - [lambdaisland/open-source](#lambdaislandopen-source)
    - [dharrigan/spotifyd-notification](#dharriganspotifyd-notification)
    - [nextjournal/ssh-github-auth](#nextjournalssh-github-auth)
    - [turtlequeue/setup-babashka](#turtlequeuesetup-babashka)
    - [interdep](#interdep)
    - [sha-words](#sha-words)
    - [adam-james-v/scripts](#adam-james-vscripts)
    - [oidc-client](#oidc-client)

Also keep an eye on the [news](news.md) page for new projects, gists and other
developments around babashka.

## Libraries

### [clj-http-lite](https://github.com/babashka/clj-http-lite)

A fork of a fork of `clj-http-lite`. Example:

``` shell
$ export BABASHKA_CLASSPATH="$(clojure -Sdeps '{:deps {clj-http-lite {:git/url "https://github.com/babashka/clj-http-lite" :sha "f44ebe45446f0f44f2b73761d102af3da6d0a13e"}}}' -Spath)"

$ bb "(require '[clj-http.lite.client :as client]) (:status (client/get \"https://www.clojure.org\"))"
200
```

### [spartan.spec](https://github.com/borkdude/spartan.spec/)

An babashka-compatible implementation of `clojure.spec.alpha`.

### [missing.test.assertions](https://github.com/borkdude/missing.test.assertions)

This library checks if no assertions have been made in a test:

``` shell
$ export BABASHKA_CLASSPATH=$(clojure -Spath -Sdeps '{:deps {borkdude/missing.test.assertions {:git/url "https://github.com/borkdude/missing.test.assertions" :sha "603cb01bee72fb17addacc53c34c85612684ad70"}}}')

$ lein bb "(require '[missing.test.assertions] '[clojure.test :as t]) (t/deftest foo) (t/run-tests)"

Testing user
WARNING: no assertions made in test foo

Ran 1 tests containing 0 assertions.
0 failures, 0 errors.
{:test 1, :pass 0, :fail 0, :error 0, :type :summary}
```

### [medley](https://github.com/weavejester/medley/)

Requires `bb` >= v0.0.71. Latest coordinates checked with with bb:

``` clojure
{:git/url "https://github.com/weavejester/medley" :sha "a4e5fb5383f5c0d83cb2d005181a35b76d8a136d"}
```

Example:

``` shell
$ export BABASHKA_CLASSPATH=$(clojure -Spath -Sdeps '{:deps {medley {:git/url "https://github.com/weavejester/medley" :sha "a4e5fb5383f5c0d83cb2d005181a35b76d8a136d"}}}')

$ bb -e "(require '[medley.core :as m]) (m/index-by :id [{:id 1} {:id 2}])"
{1 {:id 1}, 2 {:id 2}}
```

### [limit-break](https://github.com/technomancy/limit-break)

A debug REPL library.

Latest coordinates checked with with bb:

``` clojure
{:git/url "https://github.com/technomancy/limit-break" :sha "050fcfa0ea29fe3340927533a6fa6fffe23bfc2f" :deps/manifest :deps}
```

Example:

``` shell
$ export BABASHKA_CLASSPATH="$(clojure -Sdeps '{:deps {limit-break {:git/url "https://github.com/technomancy/limit-break" :sha "050fcfa0ea29fe3340927533a6fa6fffe23bfc2f" :deps/manifest :deps}}}' -Spath)"

$ bb "(require '[limit.break :as lb]) (let [x 1] (lb/break))"
Babashka v0.0.49 REPL.
Use :repl/quit or :repl/exit to quit the REPL.
Clojure rocks, Bash reaches.

break> x
1
```

### [clojure-csv](https://github.com/davidsantiago/clojure-csv)

A library for reading and writing CSV files. Note that babashka already comes
with `clojure.data.csv`, but in case you need this other library, this is how
you can use it:

``` shell
export BABASHKA_CLASSPATH="$(clojure -Sdeps '{:deps {clojure-csv {:mvn/version "RELEASE"}}}' -Spath)"

./bb -e "
(require '[clojure-csv.core :as csv])
(csv/write-csv (csv/parse-csv \"a,b,c\n1,2,3\"))
"
```

### [regal](https://github.com/lambdaisland/regal)

Requires `bb` >= v0.0.71. Latest coordinates checked with with bb:

``` clojure
{:git/url "https://github.com/lambdaisland/regal" :sha "d4e25e186f7b9705ebb3df6b21c90714d278efb7"}
```

Example:

``` shell
$ export BABASHKA_CLASSPATH=$(clojure -Spath -Sdeps '{:deps {regal {:git/url "https://github.com/lambdaisland/regal" :sha "d4e25e186f7b9705ebb3df6b21c90714d278efb7"}}}')

$ bb -e "(require '[lambdaisland.regal :as regal]) (regal/regex [:* \"ab\"])"
#"(?:\Qab\E)*"
```

### [cprop](https://github.com/tolitius/cprop/)

A clojure configuration libary. Latest test version: `"0.1.16"`.

### [comb](https://github.com/weavejester/comb)

Simple templating system for Clojure. Latest tested version: `"0.1.1"`.

``` clojure
(require '[babashka.deps :as deps])

(deps/add-deps '{:deps {comb/comb {:mvn/version "0.1.1"}}})

(require '[comb.template :as template])

(template/eval "<% (dotimes [x 3] %>foo<% ) %>") ;;=> "foofoofoo"
```

### [nubank/docopt](https://github.com/nubank/docopt.clj#babashka)

Docopt implementation in Clojure, compatible with babashka.

### [arrangement](https://github.com/greglook/clj-arrangement)

A micro-library which provides a total-ordering comparator for Clojure
values. Tested with version `1.2.0`.

### [clojure.math.combinatorics](https://github.com/clojure/math.combinatorics)

``` clojure
$ bb --classpath "$(clojure -Spath -Sdeps '{:deps {org.clojure/math.combinatorics {:mvn/version "0.1.6"}}}')" \
     -e "(use 'clojure.math.combinatorics) (permutations [:a :b])"
((:a :b) (:b :a))
```

### [testdoc](https://github.com/liquidz/testdoc)

Yet another doctest implementation in Clojure.

``` clojure
$ export BABASHKA_CLASSPATH=$(clojure -Sdeps '{:deps {testdoc {:mvn/version "1.2.0"}}}' -Spath)

$ bb '(ns foo (:use clojure.test testdoc.core))
(defn foo "
  => (foo)
  :foox"
  [] :foo)

(deftest footest
  (is (testdoc (var foo))))

(test-var (var footest))'

FAIL in (footest) (:1)
(= (foo) :foox)
expected: :foox
  actual: :foo
```

### [doric](https://github.com/joegallo/doric)

Library for printing tables.

``` clojure
$ export BABASHKA_CLASSPATH=$(clojure -Spath -Sdeps '{:deps {doric {:mvn/version "0.9.0"}}}')
$ bb "(use 'doric.core) (println (table [:a :b :c] [{:a 1 :b 2 :c 3} {:a 4 :b 5 :c 6}]))"
|---+---+---|
| A | B | C |
|---+---+---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
|---+---+---|
```

### [clojure.data.zip](https://github.com/clojure/data.zip)

Utilities for clojure.zip, among other things a more fluent way to work
with xml.

Small sample:
``` clojure
$ export BABASHKA_CLASSPATH=$(clojure -Spath -Sdeps '{:deps {org.clojure/data.zip {:mvn/version "1.0.0"}}}')

$ cat data_zip_xml.clj
(require '[clojure.data.xml :as xml])
(require '[clojure.zip :as zip])
(require '[clojure.data.zip.xml :refer [text attr attr= xml-> xml1-> text=]])

(def data (str "<root>"
               "  <character type=\"person\" name=\"alice\" />"
               "  <character type=\"animal\" name=\"march hare\" />"
               "</root>"))

(let [xml  (-> data java.io.StringReader. xml/parse zip/xml-zip)]
  (prn :alice-is-a (xml1-> xml :character [(attr= :name "alice")] (attr :type)))
  (prn :animal-is-called (xml1-> xml :character [(attr= :type "animal")] (attr :name))))

$ bb data_zip_xml.clj
:alice-is-a "person"
:animal-is-called "march hare"
```
(see for exaple [this article](https://blog.korny.info/2014/03/08/xml-for-fun-and-profit.html#datazip-for-zipper-awesomeness)
for more on clojure.data.zip).

### [clj-psql](https://github.com/DarinDouglass/clj-psql)

A small Clojure wrapper for interacting with `psql`.

```clojure
user> (psql/query conn "select name, subject from grades where grade = 100")
   => ({:name "Bobby Tables", :subject "Math"}
       {:name "Suzy Butterbean", :subject "Math"})
```

### [camel-snake-kebab](https://github.com/clj-commons/camel-snake-kebab)

A library for word case conversions.

``` clojure
(require '[babashka.deps :as deps])

(deps/add-deps '{:deps {camel-snake-kebab/camel-snake-kebab {:mvn/version "0.4.2"}}})

(require '[camel-snake-kebab.core :as csk])

(csk/->camelCase 'flux-capacitor) ;;=> 'fluxCapacitor
```

### [aero](https://github.com/juxt/aero/)

A small library for explicit, intentful configuration.

### [clojure.data.generators](https://github.com/clojure/data.generators)

Random data generators

### [honeysql](https://github.com/seancorfield/honeysql)

Turn Clojure data structures into SQL

### [bond](https://github.com/circleci/bond)

Spying and stubbing library, primarily intended for tests.

### [portal](https://github.com/djblue/portal/)

A clojure tool to navigate through your data. This example will launch a browser to view your `deps.edn`:

``` clojure
$ cat deps.edn | bb -e "(babashka.deps/add-deps '{:deps {djblue/portal {:mvn/version \"0.9.0\"}}})" \
                    -e "(require 'portal.main)" \
                    -e '(portal.main/-main "edn")'
```

Also see [examples](https://github.com/babashka/babashka/tree/master/examples#portal).

### [version-clj](https://github.com/xsc/version-clj)

Analysis and comparison of artifact version numbers.

``` clojure
> export BABASHKA_CLASSPATH=$(clojure -Spath -Sdeps '{:deps {version-clj/version-clj {:mvn/version "0.1.2"}}}')
> bb --repl
...
user=> (require '[version-clj.core :as ver])
nil
user=> (ver/version->seq "1.0.0-SNAPSHOT")
[(1 0 0) ["snapshot"]]
user=> (ver/version-compare "1.2.3" "1.0.0")
1
user=> (ver/version-compare "1.0.0-SNAPSHOT" "1.0.0")
-1
user=> (ver/version-compare "1.0" "1.0.0")
0
```

### [matchete](https://github.com/xapix-io/matchete.git)

Pattern matching library:

``` clojure
$ rlwrap bb -cp "$(clojure -Spath -Sdeps '{:deps {io.xapix/matchete {:mvn/version "1.2.0"}}}')"
user=> (require '[matchete.core :as mc])
nil
user=> (mc/matches '{?k 1} {:x 1 :y 1})"
({?k :y} {?k :x})
```

### [progrock](https://github.com/weavejester/progrock)

A functional Clojure progress bar for the command line.

Tested version: 0.1.2.

### [clj-commons/fs](https://github.com/clj-commons/fs)

File system utilities for Clojure.

``` clojure
(require '[babashka.deps :as deps])

(deps/add-deps '{:deps {clj-commons/fs {:mvn/version "1.5.2"}}})

(require '[me.raynes.fs :as fs])

(fs/link? "/tmp") ;; true
```

### [cljc.java-time](https://github.com/henryw374/cljc.java-time)

``` clojure
(require '[babashka.deps :as deps])

(deps/add-deps '{:deps {cljc.java-time/cljc.java-time {:mvn/version "0.1.12"}}})

(require  '[cljc.java-time.local-date :as ld])

(def a-date (ld/parse "2019-01-01"))

(ld/plus-days a-date 99)
```

### [environ](https://github.com/weavejester/environ)

Library for managing environment variables in Clojure.

``` clojure
(require '[babashka.deps :as deps])

(babashka.deps/add-deps '{:deps {environ/environ {:mvn/version "1.2.0"}}})

(require '[environ.core :refer [env]])

(prn (:path env))
```

### [gaka](https://github.com/cdaddr/gaka)

``` clojure
(ns script
  (:require [babashka.deps :as deps]))

(deps/add-deps '{:deps {gaka/gaka {:mvn/version "0.3.0"}}})

(require '[gaka.core :as gaka])

(def rules [:div#foo
            :margin "0px"
            [:span.bar
             :color "black"
             :font-weight "bold"
             [:a:hover
              :text-decoration "none"]]])

(println (gaka/css rules))
```

Output:

``` css
div#foo {
  margin: 0px;}

  div#foo span.bar {
    color: black;
    font-weight: bold;}

    div#foo span.bar a:hover {
      text-decoration: none;}
```

### [failjure](https://github.com/adambard/failjure)

Working with failed computations in Clojure.

``` clojure
(require '[babashka.deps :as deps])

(deps/add-deps '{:deps {failjure/failjure {:mvn/version "2.1.1"}}})

(require '[failjure.core :as f])

(f/fail "foo")
```

### [pretty](https://github.com/AvisoNovate/pretty)

The `io.aviso.ansi` namespace provides ANSI font and background color support.

``` clojure
(require '[babashka.deps :as deps])

(deps/add-deps
 '{:deps {io.aviso/pretty {:mvn/version "0.1.36"}}})

(require '[io.aviso.ansi :as ansi])

(println
 (str "The following text will be "
      ansi/bold-red-font "bold and red "
      ansi/reset-font "but this text will not."))
```

### [clojure-term-colors](https://github.com/trhura/clojure-term-colors)

Clojure ASCII color formatting for terminal output.

``` clojure
(require '[babashka.deps :as deps])

(deps/add-deps
 '{:deps {clojure-term-colors/clojure-term-colors {:mvn/version "0.1.0"}}})

(require '[clojure.term.colors :as c])

(println
 (c/yellow "Yellow")
 (c/red "Red")
 "No color")
```

### [binf](https://github.com/helins/binf.cljc)

Handling binary formats in all shapes and forms.

### [rewrite-edn](https://github.com/borkdude/rewrite-edn)

Rewrite EDN with preservation of whitespace, based on rewrite-clj.

Example:

``` clojure
#!/usr/bin/env bb

(require '[babashka.deps :as deps])
(deps/add-deps '{:deps {borkdude/rewrite-edn {:mvn/version "0.0.2"}}})
(require '[borkdude.rewrite-edn :as r])

(def edn-string (slurp "deps.edn"))
(def nodes (r/parse-string edn-string))

(println (str (r/assoc-in nodes [:deps 'my-other-dep] {:mvn/version "0.1.2"})))
```

### [expound](https://github.com/bhb/expound)

Formats `spartan.spec` error messages in a way that is optimized for humans to read.

Example:

``` clojure
#!/usr/bin/env bb

(ns expound
  (:require [babashka.deps :as deps]))

(deps/add-deps
 '{:deps {borkdude/spartan.spec {:git/url "https://github.com/borkdude/spartan.spec"
                                 :sha "bf4ace4a857c29cbcbb934f6a4035cfabe173ff1"}
          expound/expound {:mvn/version "0.8.9"}}})

;; Loading spartan.spec will create a namespace clojure.spec.alpha for compatibility:
(require 'spartan.spec)
(alias 's 'clojure.spec.alpha)

;; Expound expects some vars to be there, like `fdef`. Spartan prints warnings that these are used, but doesn't implement them yet.
(require '[expound.alpha :as expound])

(s/def ::a (s/cat :i int? :j string?))

(expound/expound ::a [1 2])
```

### [omniconf](https://github.com/grammarly/omniconf)

script.clj:
``` clojure
#!/usr/bin/env bb

(ns script
  (:require [babashka.deps :as deps]))

(deps/add-deps
 '{:deps {com.grammarly/omniconf {:mvn/version "0.4.3"}}})

(require '[omniconf.core :as cfg])
(cfg/define {:foo {}})
(cfg/populate-from-env)
(cfg/get :foo)
```

``` text
FOO=1 script.clj
Populating Omniconf from env: 1 value(s)
"1"
```

### [slingshot](https://github.com/scgilardi/slingshot)

Enhanced try and throw for Clojure leveraging Clojure's capabilities.

``` clojure
$ export BABASHKA_CLASSPATH=$(clojure -Spath -Sdeps '{:deps {slingshot/slingshot {:mvn/version "0.12.2"}}}')
$ bb -e "(require '[slingshot.slingshot :as s]) (s/try+ (s/throw+ {:type ::foo}) (catch [:type ::foo] [] 1))"
1
```

NOTE: slingshot's tests pass with babashka except one: catching a record types
by name. This is due to a difference in how records are implemented in
babashka. This may be fixed later if this turns out to be really useful.

## Pods

[Babashka pods](https://github.com/babashka/babashka.pods) are programs that can
be used as Clojure libraries by babashka. See
[pod-registry](https://github.com/babashka/pod-registry) for an overview of available pods.

Pods not available in the pod registry:

- [pod-janet-peg](https://github.com/sogaiu/pod-janet-peg): a pod for
  calling [Janet](https://github.com/janet-lang/janet)'s PEG
  functionality.
- [pod-jaydeesimon-jsoup](https://github.com/jaydeesimon/pod-jaydeesimon-jsoup):
    a pod for parsing HTML using CSS queries backed by Jsoup.
- [pod.xledger.sql-server](https://github.com/xledger/pod_sql_server): pod for interacting with SQL Server.

## Projects

### [babashka-test-action](https://github.com/marketplace/actions/babashka-test-action)

Github Action to run clojure.test by Babashka.

### [deps.clj](https://github.com/borkdude/deps.clj)

A port of the [clojure](https://github.com/clojure/brew-install/) bash script to
Clojure / babashka.

Also see [deps.clj documentation](../doc/deps.clj.md).

### [4bb](https://github.com/porkostomus/4bb)

4clojure as a babashka script!

### [babashka lambda layer](https://github.com/dainiusjocas/babashka-lambda-layer)

Babashka Lambda runtime packaged as a Lambda layer.

### [Release on push Github action](https://github.com/rymndhng/release-on-push-action)

Github Action to create a git tag + release when pushed to master. Written in
babashka.

### [justone/bb-scripts](https://github.com/justone/bb-scripts)

A collection of scripts developed by [@justone](https://github.com/justone).

### [nativity](https://github.com/MnRA/nativity)

Turn babashka scripts into binaries using GraalVM `native-image`.

### [cldwalker/bb-clis](https://github.com/cldwalker/bb-clis)

A collection of scripts developed by [@cldwalker](https://github.com/cldwalker).

### [krell template](https://github.com/ampersanda/krell-template-runner)

Babashka script for creating React Native (Krell) project

### [wee-httpd](https://github.com/bherrmann7/bb-common/blob/master/wee_httpd.bb)

A wee multi-threaded web server

### [covid19-babashka](https://github.com/agrison/covid19-babashka)

A babashka script to obtain covid-19 related information.

### [bb-spotify](https://github.com/kolharsam/bb-spotify)

Contol your spotify player using babashka.

### [lambdaisland/open-source](https://github.com/lambdaisland/open-source)

[Internal
tooling](https://github.com/babashka/babashka/issues/457#issuecomment-636739415)
used by Lambda Island projects. Noteworthy: a [babashka-compatible hiccup
script](https://github.com/lambdaisland/open-source/blob/2cfde3dfb460e72f047bf94e6f5ec7f519c6d7a0/src/lioss/hiccup.clj).

There's also
[subshell](https://github.com/lambdaisland/open-source/blob/master/src/lioss/subshell.clj)
which is like sh/sh, but it inherits stdin/stdout/stderr, so that the user sees
in real time what the subprocess is doing, and can possibly interact with
it. More like how shelling out in a bash script works.

### [dharrigan/spotifyd-notification](https://github.com/dharrigan/spotifyd-notification)

An example of using babashka to show spotifyd notifications via dunst.

### [nextjournal/ssh-github-auth](https://github.com/nextjournal/ssh-github-auth)

A babashka script which uses github auth to fetch SSH public keys. It can be useful to ensure only a certain team of people can access machines with SSH.

### [turtlequeue/setup-babashka](https://github.com/turtlequeue/setup-babashka)

Github Action to install Babashka in your workflows. Useful to run bb scripts in your CI.

### [interdep](https://github.com/rejoice-cljc/interdep)

Manage interdependent dependencies using Clojure's tools.deps and babashka.

### [sha-words](https://github.com/ordnungswidrig/sha-words)

A clojure program to turn a sha hash into list of nouns in a predictable jar.

### [adam-james-v/scripts](https://github.com/adam-james-v/scripts)

A collection of useful scripts. Mainly written with Clojure/babashka

### [oidc-client](https://gist.github.com/holyjak/ad4e1e9b863f8ed57ef0cb6ac6b30494)

Tired of being forced to use the browser every time you need to refresh an OIDC token to authenticate with a backend service? Finally there is a CLI tool for that - the babashka and Docker powered oidc_client.clj.

Upon first invocation it opens up a browser for the OIDC provider login, thereafter it caches the refresh token and uses it as long as it remains valid.
