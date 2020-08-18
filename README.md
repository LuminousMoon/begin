#include<stdio.h>

#include<math.h>

//二维热传导方程为: dT/dt = a *( d(dT/dx)/dx + d(dT/dy)/dy )    

//边界条件均采用第三类边界条件: dT/dn = h * (T - 298) / ( -k )

int main() {

	//初始数据
	int M = 20,                    //划分网格节点
		N = 10,
	double p = 7820,               //材料相关常数                        
		C = 460,
		k = 36,
		h = 2500,
		a = k / (C * p); 
	double lh = 0.2,                 //区域尺寸
		lw = 0.4d,
		ox = lw / M,
		oy = lh / N;
	double ot = 0.01,                //步长
		t = 2,                       //总时间
		S = t / ot;                  //迭代次数

	//初始温度分布规律
	double T[25][15], X[25][15];
	int x, y;
	for (x = 0; x < M; x++) {
		for (y = 0; y < N; y++) {
			T[x][y] = 353 - 22.5 *
				(((x * ox - 0.2) / 0.2) * ((x * ox - 0.2) / 0.2)
				+ ((y * oy - 0.1) / 0.1) * ((y * oy - 0.1) / 0.1));
		}
	}
	
	//计算
	{
		int s, i, j, m, n;
		for ( s = 0; s < S; s++) {
			for (i = 0; i < 20; i++) {
				for (j = 0; j < 10; j++) {
					double X[i][j] = T[i][j];
					for ( m = 1; m < M - 1; m++) {
						for ( n = 1; n < N - 1; n++) {
							T[m][n] = X[m][n] + ot * a *
								((X[m][n + 1] + X[m][n - 1] - 2 * X[m][n]) / ox * ox
								+ ((X[m + 1][n] + X[m - 1][n] - 2 * x[m][n]) / oy * oy)；
						}
					}
				}
			}

		}
	}

	//边界条件
	{
		int s, i, j;
		for (s = 0; s < S; s++) {
			for (i = 0; i < M; i++) {

			}
			for (j = 0; j < N; j++) {

			}
		}
	}


	return 0;
}
