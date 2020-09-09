## Put comments here that give an overall description of what your
## functions do

## These functions written in partial fulfillment of Coursera : R Programming : Week 3 Assignment

## There are two functions: 
#1)makeCacheMatrix: This function creates a special "matrix" object that can cache its inverse.

makeCacheMatrix <- function(x = matrix()) {  # matrix argument
  inv <- NULL                                # define inverse as NUll
  set <- function(y) {                       # define the set function to assign new 
    x <<- y                                  # value of matrix in parent environment.
  inv <<- NULL                               # if there is a new matrix, again set inverse to NULL
  }
  get <- function()x                         # get fucntion - returns value of the matrix argument
  setInverse <- function(inverse) inv <<- inverse   # assigns value of inv in parent environment
  getInverse <- function() inv
  list(set = set, get = get, 
       setInverse = setInverse, 
       getInverse = getInverse)
}

#2)cacheSolve: This function computes the inverse of the special "matrix"
## returned by makeCacheMatrix above.

cacheSolve <- function(x, ...) {        # Return a matrix that is the inverse of 'x'
  inv <- x$getInverse()
  if(!is.null(inv)) {
    message("getting cached data")
    return(inv)                         # Returns inverse value
  }
  data <- x$get()
  inv <- solve(data, ...)               # calculates inverse value
  x$setInverse(inv)
  inv      
}
