this is the full code of the homework 4-1

```python
import math
import numpy as np
import matplotlib.pyplot as plt

#Normal(0,1)建置
def Phi(x: float) -> float:
    return 0.5 * (1.0 + math.erf(x / math.sqrt(2.0)))

#beta值的計算（OC function)
def beta_two_sided(n: int, k: float, z: float = 3.0) -> float:
    delta = k * math.sqrt(n)          
    return Phi(z - delta) - Phi(-z - delta)

def main():
    z = 3.0
    n_list = [3, 5, 10, 15, 20]
    k_max, k_step = 3.0, 0.01
    k_grid = np.arange(0.0, k_max + 1e-12, k_step)

    plt.figure(figsize=(8, 5))
    for n in n_list:
        betas = [beta_two_sided(n, k, z) for k in k_grid]
        plt.plot(k_grid, betas, label=f"n={n}")

    alpha = 2.0 * (1.0 - Phi(z))  #算alpha的值
    plt.axhline(1 - alpha, linestyle="--", linewidth=1.0, label=f"1-α≈{1-alpha:.3f}")

    plt.title("OC Curve (β vs k) — Two-Sided 3σ X̄-Chart")
    plt.xlabel("Shift k   (μ1 = μ0 + k·σ0)")
    plt.ylabel("β = P(fail to signal)")
    plt.ylim(0, 1)
    plt.xlim(0, k_max)
    plt.grid(True, alpha=0.3)
    plt.legend(title="Sample size", ncol=2)
    plt.tight_layout()
    plt.savefig("homework_4-1.png", dpi=200)
    

if __name__ == "__main__":
    main()

