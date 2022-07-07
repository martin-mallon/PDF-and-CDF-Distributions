<h1>Probability Mass Functions (PMF) & Cumulative Density Functions (CDF)</h1>

<br>

<p align="center" width="100%">
    <img width="100%" src="/PDF_&_CDF_Distributions/pmf_cdf.png"
</p>

<br>

<h3>Overview</h3>
  
<p>Probability Mass Functions (PMF) & Cumulative Density Functions (CDF) are used to analyse distributions. PMF is the probability of observing a specific discrete variable from a population, while CDF defines the probability of an observation that is less than or equal to a discrete variable. In essesence, the PDF answers, <i>what is the probability of x?</i>, and the CDF answers, <i>what is the probability of <= x?</i> This project uses the <code>empiricaldist</code> library to transform a DataFrame into a PMF or CDF and visualise the results.</p>


<br>

<h3>PMF</h3>
  
<ul>
    <li><code>pmf</code> - Three arguments are required by the <code>pmf</code> function:</li>
    <ul>
        <li><code>data</code> - DataFrame</li>
        <li><code>col</code> - Field name from the DataFrame.</li>
        <li><code>norm</code> - Boolean value.</li>
    </ul>
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

# run
pmf_educ = pmf(df, 'educ', True)
pmf_educ.head(5)
```

<p align="center" width="100%">
    <img width="75%" src="/PDF_&_CDF_Distributions/pmf_func.png"
</p>

<br>

<h3>CDF</h3>
  
<ul>
    <li><code>cdf</code> - Three arguments are required by the <code>cdf</code> function:</li>
    <ul>
        <li><code>data</code> - DataFrame</li>
        <li><code>col</code> - Field name from the DataFrame.</li>
        <li><code>norm</code> - Boolean value.</li>
    </ul>
</ul>

```Python
# cumulative distribution function
def cdf(data, col, norm):
    
    from empiricaldist import Cdf
    cdf = Cdf.from_seq(data[col], normalize=norm)
    
    cdf = pd.DataFrame(cdf)
    cdf.reset_index(inplace=True)
    cdf.columns = [col, 'probs']
    
    return cdf

# run
cdf_educ = cdf(df, 'educ', True)
cdf_educ.head(5)
```

<p align="center" width="100%">
    <img width="75%" src="/PDF_&_CDF_Distributions/cdf_func.png"
</p>

<br>

<h3>Viz</h3>

<ul>
    <li><code>Data viz</code> - Functions are used to visualise the results (as shown above).</li>
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

#cdf line
def cdf_line(ax, data, x, y, c, legloc):
    sns.lineplot(ax=ax, data=data, x=x, y=y, color=c, label='CDF')
    ax.set_title(f'CDF: {x}')
    ax.set_xlabel(x)
    ax.set_ylabel('Cumulative Distribution Function (CDF)')
    ax.legend(loc=legloc)
    return ax
```
