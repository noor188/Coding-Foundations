;; The first three lines of this file were inserted by DrRacket. They record metadata
;; about the language level of this file in a form that our tools can easily process.
#reader(lib "htdp-beginner-reader.ss" "lang")((modname Naturals-and-Helpers) (read-case-sensitive #t) (teachpacks ()) (htdp-settings #(#t constructor repeating-decimal #f #t none #f () #f)))
(require 2htdp/image)
;; Test tube with blobs

;; ======================================================================
;; Data Definitions

;; Blob is one of:
;; - "Solid"
;; - "Fluid"
;; interp. the physical status of a blob

(define B0 "Solid")
(define B1 "Fluid")
#;
(define (fn-for-blob b)
  (cond [(string=? b "Solid") (...)]
        [(string=? b "Fluid") (...)]))

;; ListOfBlob is one of:
;; - empty
;; - (cons Blob ListOfBlob)
;; interp. list of blobs

(define LOB-1 empty)
(define LOB-2 (cons "Solid" empty))
(define LOB-3 (cons "Fluid" LOB-2))
#;
(define (fn-for-lob lob)
  (cond [(empty? lob) (...)]
        [else
         (... (fn-for-blob(first lob))     ; Blob
              (fn-for-lob(rest  lob)))]))  ; ListOfBlob

;; ======================================================================
;; Functions

;; ListOfBlob -> ListOfBlob
;; Sinks each solid blob by one
(check-expect (sink empty) empty)
(check-expect (sink (cons "bubble" (cons "solid" (cons "bubble" empty))))
              (cons "bubble" (cons "bubble" (cons "solid" empty))))
(check-expect (sink (cons "solid" (cons "solid" (cons "bubble" empty))))
              (cons "bubble" (cons "solid" (cons "solid" empty))))
(check-expect (sink (cons "solid" (cons "bubble" (cons "bubble" empty))))
              (cons "bubble" (cons "solid" (cons "bubble" empty))))
(check-expect (sink (cons "solid" (cons "bubble" (cons "solid" empty))))
              (cons "bubble" (cons "solid" (cons "solid" empty))))
(check-expect (sink (cons "bubble" (cons "solid" (cons "solid" empty))))
              (cons "bubble" (cons "solid" (cons "solid" empty))))
(check-expect (sink (cons "solid"
                          (cons "solid"
                                (cons "bubble" (cons "bubble" empty)))))
              (cons "bubble" (cons "solid" 
                                   (cons "solid" (cons "bubble" empty)))))
(define (sink lob) lob); stub
