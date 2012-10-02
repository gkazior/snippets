
(defmacro triple-cmd [cmd] (list 'do cmd cmd cmd))

(triple-cmd (print "he ")) ;; he he he

(defmacro triple-cmd-v2 [cmd] `(do ~cmd ~cmd ~cmd))
(triple-cmd-v2 (print "he ")) ;; he he he


(macroexpand '(triple-cmd-v2 (print "he ")))
