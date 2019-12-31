## learning clojure

I will only concentrate on clojurescript for now because everything JVM might be beyond me.

lumo is SELF HOSTED - which means it can't contain any JVM components.  realistically it means you cant use `core.async` - there is an alrernative lib called `andare` which can be used.
 for the most part when using `lumo` you will install dependencies through npm


### errors

when using andare with lumo, with the following lumo file

```
(require '[lumo.build.api :as b])

(b/watch "src"
         {:main 'read.core
          :output-to "watch/main.js"
          :output-dir "watch"
          :optimizations :advanced
          :verbose true
          :foreign-libs [{:file "src"
                          :module-type :es6}]
          :watch-fn (fn [] (println "Updated build"))
          :target :nodejs})
```

it would work once, but on second compile without deleting `watch/` the following error would happen
```
#error {:message failed compiling file:src/read/core.cljs, :data {:file src/read/core.cljs}, :cause #error {:message Could not require cljs.core.async, :data {:tag :cljs/analysis-error}, :cause #object[Error Error: No *eval-fn* set]}}
```


I haven't actually been able to fix this yet.  The watch just doesn't work - I have to delete the watch folder every single time i want to regenerate the resources.


this tutorial [seems very good about showing how core.async actually works](https://www.bradcypert.com/clojure-async/)
