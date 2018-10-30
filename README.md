# RcppArmadillo reference guide

## Example

```c++
// [[Rcpp::depends(RcppArmadillo)]]

#include <RcppArmadillo.h>
using namespace Rcpp;

// [[Rcpp::export]]
List fastLm(const arma::vec & y, const arma::mat & X) {

    int n = X.n_rows, k = X.n_cols;
   
    arma::colvec coef = arma::solve(X, y); 
    arma::colvec resid = y - X*coef; 
   
    double sig2 = arma::as_scalar(arma::trans(resid)*resid/(n-k));
    arma::colvec stderrest = 
        arma::sqrt(sig2 * arma::diagvec( arma::inv(arma::trans(X)*X)) );
   
   return List::create(Named("coefficients") = coef,
                       Named("stderr")       = stderrest);
}
```

## Call Rcpp function defined in another script
[SO link](https://stackoverflow.com/questions/15891781/how-to-call-on-a-function-found-on-another-file)

## Contact

Spencer Woody (email: `spencer.woody@utexas.edu`)

   
