| Resource    |  Github Actions      |  Code Coverage  |
| ----------  | -------------------- | --------------- |
| Platforms   | Windows, macOS, Linux|    codecov      |
| R CMD check | [![R build status](https://github.com/NSAPH-Software/GPCERF/workflows/R-CMD-check/badge.svg)](https://github.com/NSAPH-Software/GPCERF/actions) | [![codecov](https://codecov.io/gh/NSAPH-Software/GPCERF/branch/develop/graph/badge.svg?token=066ISL822N)](https://app.codecov.io/gh/NSAPH-Software/GPCERF) |


# Gaussian processes for the estimation of causal exposure-response curves (GP-CERF)

## Summary
Gaussian Process (GP) approach for nonparametric modeling. 

## Installation

```r
library("devtools")
install_github("NSAPH-Software/GPCERF", ref="develop")
library("GPCERF")
```

## Usage


```r
  sim_data <- generate_synthetic_data(sample_size = 500, gps_spec = 3)

  # Estimate GPS function
  # In the future, CausalGPS gps estimation will be used.
  GPS_m <- train_GPS(cov_mt = as.matrix(sim_data[,-(1:2)]),
                     w_all = as.matrix(sim_data$treat))

  # exposure values
  w_all <- seq(0,20,0.1)

  data.table::setDT(sim_data)

  cerf_gp_obj <- estimate_cerf_gp(sim_data,
                                  w_all,
                                  GPS_m,
                                  params = list(alpha = c(0.1,0.2,0.4),
                                                beta=0.2,
                                                g_sigma = 1,
                                                tune_app = "all"),
                                  nthread = 1)

```

## References

Ren, B., Wu, X., Braun, D., Pillai, N. and Dominici, F., 2021. Bayesian modeling for exposure response curve via gaussian processes: Causal effects of exposure to air pollution on health outcomes. arXiv preprint arXiv:2105.03454.
