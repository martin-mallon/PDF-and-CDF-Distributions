<h1>Probability Mass Functions (PMF) & Cumulative Density Functions (CDF)</h1>

<br>

<p align="center" width="100%">
    <img width="100%" src="/PDF_&_CDF_Distributions/pmf_cdf.png"
</p>

<br>

<h3>Overview</h3>
  
<p>The National Survey of Family Growth (NSFG) gathers information on family life, marriage and divorce, pregnancy, infertility, use of contraception, and men’s and women’s health. Results data from 2020 demostrates how pre-term babies are on average lighter than their full-term counterparts.</p>


<br>

<h3>PMF</h3>
  
<ul>
    <li><code>PMF</code> - </li>
</ul>

```Python
# probability mass function
def pmf(data, col, norm):
    
    from empiricaldist import Pmf
    pmf = Pmf.from_seq(data[col], normalize=norm)
    
    pmf = pd.DataFrame(pmf)
    pmf.reset_index(inplace=True)
    pmf.columns = [col, 'probs']
    
    return pmf
```


<ul>
    <li><code>PMF viz</code> - </li>
</ul>

```Python
# pmf bar
def pmf_bar(ax, data, x, y, c, legloc):
    sns.barplot(ax=ax, data=data, x=x, y=y, color=c, label='PMF', alpha=0.5)
    ax.set_title(f'PMF: {x}')
    ax.set_xlabel(x)
    ax.set_ylabel('Probability Mass Function (PDF)')
    ax.legend(loc=legloc)
    return ax
```
