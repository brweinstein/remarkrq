# remarkrq

I received 1/5 marks on Q8.c). I believe my solution is correct based on how the questions were stated.

The comments I received were:
"Black-hole check must be colour-specific and use <= 0 after (- (star-fuel star) (* rate n))"
"Return the rebuilt star directly (no recursion with n=0), include an else for other colours and never return a start with negative fuel".

The question description does not state not to use recursion in this format and the data definition for star contains fuel as a num which does not state it must be non-negative. This implementation also ensures a star with negative fuel is never returned, but instead 'blackhole will be. Since we require a star to be passed into the function, only the valid colours should be provided as we want the function to error if an invalid star is provided.

Consider the below racket code. This is the implementation of my star-time function and passes the below tests.

Thank you for your time! I would be happy to learn from my mistakes or hear further feedback.
```
(define (star-time star n)
  (cond
    [(zero? n)
     (cond [(>= 0 (star-fuel star)) 'blackhole]
           [else star])]
    [(symbol=? (star-colour star) 'blue)
     (star-time (mk-star 'blue (star-points star) (- (star-fuel star) (* 3 n))) 0)]
    [(symbol=? (star-colour star) 'orange)
     (star-time (mk-star 'blue (star-points star) (- (star-fuel star) (* 4 n))) 0)]
    [(symbol=? (star-colour star) 'red)
     (star-time (mk-star 'blue (star-points star) (- (star-fuel star) (* 5 n))) 0)]))

(define (mk-star sym n k)
  (cons sym (cons n (cons k empty))))

(define (star-colour star)
  (first star))

(define (star-points star)
  (first (rest star)))

(define (star-fuel star)
  (first (rest (rest star))))

(define my_star (mk-star 'blue 4 9))

(check-expect (star-time my_star 3) 'blackhole); fuel is zero
(check-expect (star-time my_star 4) 'blackhole); fuel is less than zero (out of fuel)
(check-expect (star-time my_star 2)
              (mk-star 'blue 4 3))
```
