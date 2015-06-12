# Company-arduino.el
This package is a set of configuration to let you auto-completion
by using `irony-mode`, `company-irony` and `company-c-headers` on arduino-mode.

## Prerequisite
This package need irony-mode, company-irony and company-c-headers
packages. Please install those packages first. But if you are using
MELPA, package.el will install dependencies automatically when you install
this package. Also, you need irony-mode's setting, so please follow
the irony-mode's instruction (https://github.com/Sarcasm/irony-mode).

## Usage
Set $ARDUINO_HOME environment variable as Arduino IDE's installed directory.  

    export ARDUINO_HOME=$HOME/share/devkit/arduino-1.6.3

Then put following configurations to your .emacs or somewhere.

```lisp
;; If you installed this package from without MELPA, you may need
;; `(require 'company-arduino)'.
  
;; Configuration for irony.el
;; Add arduino's include options to irony-mode's variable.
(add-hook 'irony-mode-hook 'company-arduino-turn-on)
  
;; Configuration for company-c-headers.el
;; The `company-arduino-append-include-dirs' function appends
;; Arduino's include directories to the default directories
;; if `default-directory' is inside `company-arduino-home'. Otherwise
;; just returns the default directories.
;; Please change the default include directories accordingly.
(defun my-company-c-headers-get-system-path ()
  "Return the system include path for the current buffer."
  (let ((default '("/usr/include/" "/usr/local/include/")))
    (company-arduino-append-include-dirs default t)))
(setq company-c-headers-path-system 'my-company-c-headers-get-system-path)
```

## Note
This package's default configuration is set for Linux environment,
which I'm currently using, so if you are using different
environment (Mac or Windows), please change the Arduino's directory paths accordingly.
Related variables: `company-arduino-sketch-directory-regex`, `company-arduino-home`,
`company-arduino-header`, `company-arduino-includes-dirs` and `irony-arduino-includes-options`.

## Pull-Requests are welcome
I'm a beginner of Arduino, so if you notice something wrong or have
opinion to improve this package, let me know via GitHub issues:)
