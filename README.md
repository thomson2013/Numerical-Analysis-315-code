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
  
        function z = PoissonSolve(n,f)
        z = zeros(n,1); 
        A = zeros(n,n);
        h = 1/(n+1);
        sum = 0;
        for i = 1:n
                sum = sum + (i*f(i));
        end
        z(n) = (sum*(h^2))/(n+1);
        for i = (n-1):-1:1
                if i == n-1
                        z(i) = (2*z(i+1))-(f(i+1)*(h^2));
                else
                        z(i) = (2*z(i+1))-z(i+2)-(f(i+1)*(h^2));
                end
        end
        
  Naive Poisson solver and timer
      
        n=100;
        %n is the size of the matrix and length of f
        f = zeros(n,1);
        for i = 1:n
                f(i) = sin(i/2*pi);
        end
        A = PoissonMat(n);
        tic
        h = 1/(n+1);
        b = h*h*f;
        y = A \ b;
        NaiveTime = toc
        
        tic
        z = PoissonSolve(n,f);
        fastTime = toc
       
  
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
 
