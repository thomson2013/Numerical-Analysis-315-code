# Numerical-Analysis-315-code
Contains the code for the PoissonMat, PoissonSolve, and Wilkinson functions

  PoissonMat function:
  
  function A = PoissonMat(n)
  A = zeros(n,n);
  for i = 1:n
    if (i+1) <= n
        A(i,i+1) = -1;
    end
    if (i-1) > 0
        A(i,i-1) = -1;
    end
    A(i,i) = 2;
  end

  PoissonSolve function:
  
  
  
  Wilkinson function:
  
  function W = wilkin(n)
  %Computes a nxn Wilkinson matrix
  A = zeros(n,n);
  for i = 1:n
    A(i,n) = 1;
    A(i,i) = 1;
    for j = 1:n
        if i > j
            A(i,j) = -1;
        end
    end
  end
 
