{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Prueba tecnica Daniel Cordoba"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Primer Punto:"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "##### Los puntos correspondientes a estadisticas descriptivas fueron desarrollados en un tablero en powerBi, para visualizarlo deben ingresar a este [enlace](https://app.powerbi.com/view?r=eyJrIjoiMDNkMTZmNzUtMThiZS00ODcyLWJkMzQtMWEwMmMyN2FlYTM0IiwidCI6IjcxOGE2MTYzLWE5YzYtNDdlMi1iYzRjLTZmMjRmMGJjMjYyYyJ9&pageName=ReportSection)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "##### En resumen, tenemos que el monto promedio general del monto de prestamo es igual a USD$16360.\n",
    "##### A detalle en la primera pagina se pueden ver estos valores desagregados por el Estado donde fue emitido y el proposito del prestamo. Ademas en la tabla donde esta la caracteristica del Estado, podemos ver si la persona es dueña, inquilina o tiene una hipoteca con el inmueble en donde vive."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<br>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Segundo Punto:"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "##### En general el proposito del prestamo que mas se solicita es una consolidacion de deuda, seguido por tarjetas de credito."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<br>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Tercer Punto:"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "##### Los montos promedios con respecto al uso final del prestamo, esta ranqueado con respecto a las siguientes categorias:\n",
    "- Crear un negocio pequeño.\n",
    "- Comprar una Casa.\n",
    "- Consolidar Deuda.\n",
    "- Arreglos o mejoras a la casa."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<br>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Cuarto Punto:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "library(dplyr)\n",
    "library(h2o)\n",
    "library(h2o)\n",
    "library(xtable)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "DATA = read.csv(\"D:/2021_1/prueba_blacksmith/lending_club.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table>\n",
       "<caption>A data.frame: 6 × 55</caption>\n",
       "<thead>\n",
       "\t<tr><th></th><th scope=col>emp_title</th><th scope=col>emp_length</th><th scope=col>state</th><th scope=col>homeownership</th><th scope=col>annual_income</th><th scope=col>verified_income</th><th scope=col>debt_to_income</th><th scope=col>annual_income_joint</th><th scope=col>verification_income_joint</th><th scope=col>debt_to_income_joint</th><th scope=col>...</th><th scope=col>sub_grade</th><th scope=col>issue_month</th><th scope=col>loan_status</th><th scope=col>initial_listing_status</th><th scope=col>disbursement_method</th><th scope=col>balance</th><th scope=col>paid_total</th><th scope=col>paid_principal</th><th scope=col>paid_interest</th><th scope=col>paid_late_fees</th></tr>\n",
       "\t<tr><th></th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>...</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>\n",
       "</thead>\n",
       "<tbody>\n",
       "\t<tr><th scope=row>1</th><td>global config engineer </td><td> 3</td><td>NJ</td><td>MORTGAGE</td><td>90000</td><td>Verified       </td><td>18.01</td><td>   NA</td><td>        </td><td>   NA</td><td>...</td><td>C3</td><td>mar-18  </td><td>Current</td><td>whole     </td><td>Cash</td><td>27015.86</td><td>1999.33</td><td> 984.14</td><td>1015.19</td><td>0</td></tr>\n",
       "\t<tr><th scope=row>2</th><td>warehouse office clerk </td><td>10</td><td>HI</td><td>RENT    </td><td>40000</td><td>Not Verified   </td><td> 5.04</td><td>   NA</td><td>        </td><td>   NA</td><td>...</td><td>C1</td><td>feb-18  </td><td>Current</td><td>whole     </td><td>Cash</td><td> 4651.37</td><td> 499.12</td><td> 348.63</td><td> 150.49</td><td>0</td></tr>\n",
       "\t<tr><th scope=row>3</th><td>assembly               </td><td> 3</td><td>WI</td><td>RENT    </td><td>40000</td><td>Source Verified</td><td>21.15</td><td>   NA</td><td>        </td><td>   NA</td><td>...</td><td>D1</td><td>feb-18  </td><td>Current</td><td>fractional</td><td>Cash</td><td> 1824.63</td><td> 281.80</td><td> 175.37</td><td> 106.43</td><td>0</td></tr>\n",
       "\t<tr><th scope=row>4</th><td>customer service       </td><td> 1</td><td>PA</td><td>RENT    </td><td>30000</td><td>Not Verified   </td><td>10.16</td><td>   NA</td><td>        </td><td>   NA</td><td>...</td><td>A3</td><td>Jan-2018</td><td>Current</td><td>whole     </td><td>Cash</td><td>18853.26</td><td>3312.89</td><td>2746.74</td><td> 566.15</td><td>0</td></tr>\n",
       "\t<tr><th scope=row>5</th><td>security supervisor    </td><td>10</td><td>CA</td><td>RENT    </td><td>35000</td><td>Verified       </td><td>57.96</td><td>57000</td><td>Verified</td><td>37.66</td><td>...</td><td>C3</td><td>mar-18  </td><td>Current</td><td>whole     </td><td>Cash</td><td>21430.15</td><td>2324.65</td><td>1569.85</td><td> 754.80</td><td>0</td></tr>\n",
       "\t<tr><th scope=row>6</th><td>                       </td><td>NA</td><td>KY</td><td>OWN     </td><td>34000</td><td>Not Verified   </td><td> 6.46</td><td>   NA</td><td>        </td><td>   NA</td><td>...</td><td>A3</td><td>Jan-2018</td><td>Current</td><td>whole     </td><td>Cash</td><td> 4256.71</td><td> 873.13</td><td> 743.29</td><td> 129.84</td><td>0</td></tr>\n",
       "</tbody>\n",
       "</table>\n"
      ],
      "text/latex": [
       "A data.frame: 6 × 55\n",
       "\\begin{tabular}{r|lllllllllllllllllllll}\n",
       "  & emp\\_title & emp\\_length & state & homeownership & annual\\_income & verified\\_income & debt\\_to\\_income & annual\\_income\\_joint & verification\\_income\\_joint & debt\\_to\\_income\\_joint & ... & sub\\_grade & issue\\_month & loan\\_status & initial\\_listing\\_status & disbursement\\_method & balance & paid\\_total & paid\\_principal & paid\\_interest & paid\\_late\\_fees\\\\\n",
       "  & <fct> & <int> & <fct> & <fct> & <dbl> & <fct> & <dbl> & <dbl> & <fct> & <dbl> & ... & <fct> & <fct> & <fct> & <fct> & <fct> & <dbl> & <dbl> & <dbl> & <dbl> & <dbl>\\\\\n",
       "\\hline\n",
       "\t1 & global config engineer  &  3 & NJ & MORTGAGE & 90000 & Verified        & 18.01 &    NA &          &    NA & ... & C3 & mar-18   & Current & whole      & Cash & 27015.86 & 1999.33 &  984.14 & 1015.19 & 0\\\\\n",
       "\t2 & warehouse office clerk  & 10 & HI & RENT     & 40000 & Not Verified    &  5.04 &    NA &          &    NA & ... & C1 & feb-18   & Current & whole      & Cash &  4651.37 &  499.12 &  348.63 &  150.49 & 0\\\\\n",
       "\t3 & assembly                &  3 & WI & RENT     & 40000 & Source Verified & 21.15 &    NA &          &    NA & ... & D1 & feb-18   & Current & fractional & Cash &  1824.63 &  281.80 &  175.37 &  106.43 & 0\\\\\n",
       "\t4 & customer service        &  1 & PA & RENT     & 30000 & Not Verified    & 10.16 &    NA &          &    NA & ... & A3 & Jan-2018 & Current & whole      & Cash & 18853.26 & 3312.89 & 2746.74 &  566.15 & 0\\\\\n",
       "\t5 & security supervisor     & 10 & CA & RENT     & 35000 & Verified        & 57.96 & 57000 & Verified & 37.66 & ... & C3 & mar-18   & Current & whole      & Cash & 21430.15 & 2324.65 & 1569.85 &  754.80 & 0\\\\\n",
       "\t6 &                         & NA & KY & OWN      & 34000 & Not Verified    &  6.46 &    NA &          &    NA & ... & A3 & Jan-2018 & Current & whole      & Cash &  4256.71 &  873.13 &  743.29 &  129.84 & 0\\\\\n",
       "\\end{tabular}\n"
      ],
      "text/markdown": [
       "\n",
       "A data.frame: 6 × 55\n",
       "\n",
       "| <!--/--> | emp_title &lt;fct&gt; | emp_length &lt;int&gt; | state &lt;fct&gt; | homeownership &lt;fct&gt; | annual_income &lt;dbl&gt; | verified_income &lt;fct&gt; | debt_to_income &lt;dbl&gt; | annual_income_joint &lt;dbl&gt; | verification_income_joint &lt;fct&gt; | debt_to_income_joint &lt;dbl&gt; | ... ... | sub_grade &lt;fct&gt; | issue_month &lt;fct&gt; | loan_status &lt;fct&gt; | initial_listing_status &lt;fct&gt; | disbursement_method &lt;fct&gt; | balance &lt;dbl&gt; | paid_total &lt;dbl&gt; | paid_principal &lt;dbl&gt; | paid_interest &lt;dbl&gt; | paid_late_fees &lt;dbl&gt; |\n",
       "|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|\n",
       "| 1 | global config engineer  |  3 | NJ | MORTGAGE | 90000 | Verified        | 18.01 |    NA | <!----> |    NA | ... | C3 | mar-18   | Current | whole      | Cash | 27015.86 | 1999.33 |  984.14 | 1015.19 | 0 |\n",
       "| 2 | warehouse office clerk  | 10 | HI | RENT     | 40000 | Not Verified    |  5.04 |    NA | <!----> |    NA | ... | C1 | feb-18   | Current | whole      | Cash |  4651.37 |  499.12 |  348.63 |  150.49 | 0 |\n",
       "| 3 | assembly                |  3 | WI | RENT     | 40000 | Source Verified | 21.15 |    NA | <!----> |    NA | ... | D1 | feb-18   | Current | fractional | Cash |  1824.63 |  281.80 |  175.37 |  106.43 | 0 |\n",
       "| 4 | customer service        |  1 | PA | RENT     | 30000 | Not Verified    | 10.16 |    NA | <!----> |    NA | ... | A3 | Jan-2018 | Current | whole      | Cash | 18853.26 | 3312.89 | 2746.74 |  566.15 | 0 |\n",
       "| 5 | security supervisor     | 10 | CA | RENT     | 35000 | Verified        | 57.96 | 57000 | Verified | 37.66 | ... | C3 | mar-18   | Current | whole      | Cash | 21430.15 | 2324.65 | 1569.85 |  754.80 | 0 |\n",
       "| 6 | <!----> | NA | KY | OWN      | 34000 | Not Verified    |  6.46 |    NA | <!----> |    NA | ... | A3 | Jan-2018 | Current | whole      | Cash |  4256.71 |  873.13 |  743.29 |  129.84 | 0 |\n",
       "\n"
      ],
      "text/plain": [
       "  emp_title               emp_length state homeownership annual_income\n",
       "1 global config engineer   3         NJ    MORTGAGE      90000        \n",
       "2 warehouse office clerk  10         HI    RENT          40000        \n",
       "3 assembly                 3         WI    RENT          40000        \n",
       "4 customer service         1         PA    RENT          30000        \n",
       "5 security supervisor     10         CA    RENT          35000        \n",
       "6                         NA         KY    OWN           34000        \n",
       "  verified_income debt_to_income annual_income_joint verification_income_joint\n",
       "1 Verified        18.01             NA                                        \n",
       "2 Not Verified     5.04             NA                                        \n",
       "3 Source Verified 21.15             NA                                        \n",
       "4 Not Verified    10.16             NA                                        \n",
       "5 Verified        57.96          57000               Verified                 \n",
       "6 Not Verified     6.46             NA                                        \n",
       "  debt_to_income_joint ... sub_grade issue_month loan_status\n",
       "1    NA                ... C3        mar-18      Current    \n",
       "2    NA                ... C1        feb-18      Current    \n",
       "3    NA                ... D1        feb-18      Current    \n",
       "4    NA                ... A3        Jan-2018    Current    \n",
       "5 37.66                ... C3        mar-18      Current    \n",
       "6    NA                ... A3        Jan-2018    Current    \n",
       "  initial_listing_status disbursement_method balance  paid_total paid_principal\n",
       "1 whole                  Cash                27015.86 1999.33     984.14       \n",
       "2 whole                  Cash                 4651.37  499.12     348.63       \n",
       "3 fractional             Cash                 1824.63  281.80     175.37       \n",
       "4 whole                  Cash                18853.26 3312.89    2746.74       \n",
       "5 whole                  Cash                21430.15 2324.65    1569.85       \n",
       "6 whole                  Cash                 4256.71  873.13     743.29       \n",
       "  paid_interest paid_late_fees\n",
       "1 1015.19       0             \n",
       "2  150.49       0             \n",
       "3  106.43       0             \n",
       "4  566.15       0             \n",
       "5  754.80       0             \n",
       "6  129.84       0             "
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "head(DATA)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<style>\n",
       ".list-inline {list-style: none; margin:0; padding: 0}\n",
       ".list-inline>li {display: inline-block}\n",
       ".list-inline>li:not(:last-child)::after {content: \"\\00b7\"; padding: 0 .5ex}\n",
       "</style>\n",
       "<ol class=list-inline><li>'emp_title'</li><li>'emp_length'</li><li>'state'</li><li>'homeownership'</li><li>'annual_income'</li><li>'verified_income'</li><li>'debt_to_income'</li><li>'annual_income_joint'</li><li>'verification_income_joint'</li><li>'debt_to_income_joint'</li><li>'delinq_2y'</li><li>'months_since_last_delinq'</li><li>'earliest_credit_line'</li><li>'inquiries_last_12m'</li><li>'total_credit_lines'</li><li>'open_credit_lines'</li><li>'total_credit_limit'</li><li>'total_credit_utilized'</li><li>'num_collections_last_12m'</li><li>'num_historical_failed_to_pay'</li><li>'months_since_90d_late'</li><li>'current_accounts_delinq'</li><li>'total_collection_amount_ever'</li><li>'current_installment_accounts'</li><li>'accounts_opened_24m'</li><li>'months_since_last_credit_inquiry'</li><li>'num_satisfactory_accounts'</li><li>'num_accounts_120d_past_due'</li><li>'num_accounts_30d_past_due'</li><li>'num_active_debit_accounts'</li><li>'total_debit_limit'</li><li>'num_total_cc_accounts'</li><li>'num_open_cc_accounts'</li><li>'num_cc_carrying_balance'</li><li>'num_mort_accounts'</li><li>'account_never_delinq_percent'</li><li>'tax_liens'</li><li>'public_record_bankrupt'</li><li>'loan_purpose'</li><li>'application_type'</li><li>'loan_amount'</li><li>'term'</li><li>'interest_rate'</li><li>'installment'</li><li>'grade'</li><li>'sub_grade'</li><li>'issue_month'</li><li>'loan_status'</li><li>'initial_listing_status'</li><li>'disbursement_method'</li><li>'balance'</li><li>'paid_total'</li><li>'paid_principal'</li><li>'paid_interest'</li><li>'paid_late_fees'</li></ol>\n"
      ],
      "text/latex": [
       "\\begin{enumerate*}\n",
       "\\item 'emp\\_title'\n",
       "\\item 'emp\\_length'\n",
       "\\item 'state'\n",
       "\\item 'homeownership'\n",
       "\\item 'annual\\_income'\n",
       "\\item 'verified\\_income'\n",
       "\\item 'debt\\_to\\_income'\n",
       "\\item 'annual\\_income\\_joint'\n",
       "\\item 'verification\\_income\\_joint'\n",
       "\\item 'debt\\_to\\_income\\_joint'\n",
       "\\item 'delinq\\_2y'\n",
       "\\item 'months\\_since\\_last\\_delinq'\n",
       "\\item 'earliest\\_credit\\_line'\n",
       "\\item 'inquiries\\_last\\_12m'\n",
       "\\item 'total\\_credit\\_lines'\n",
       "\\item 'open\\_credit\\_lines'\n",
       "\\item 'total\\_credit\\_limit'\n",
       "\\item 'total\\_credit\\_utilized'\n",
       "\\item 'num\\_collections\\_last\\_12m'\n",
       "\\item 'num\\_historical\\_failed\\_to\\_pay'\n",
       "\\item 'months\\_since\\_90d\\_late'\n",
       "\\item 'current\\_accounts\\_delinq'\n",
       "\\item 'total\\_collection\\_amount\\_ever'\n",
       "\\item 'current\\_installment\\_accounts'\n",
       "\\item 'accounts\\_opened\\_24m'\n",
       "\\item 'months\\_since\\_last\\_credit\\_inquiry'\n",
       "\\item 'num\\_satisfactory\\_accounts'\n",
       "\\item 'num\\_accounts\\_120d\\_past\\_due'\n",
       "\\item 'num\\_accounts\\_30d\\_past\\_due'\n",
       "\\item 'num\\_active\\_debit\\_accounts'\n",
       "\\item 'total\\_debit\\_limit'\n",
       "\\item 'num\\_total\\_cc\\_accounts'\n",
       "\\item 'num\\_open\\_cc\\_accounts'\n",
       "\\item 'num\\_cc\\_carrying\\_balance'\n",
       "\\item 'num\\_mort\\_accounts'\n",
       "\\item 'account\\_never\\_delinq\\_percent'\n",
       "\\item 'tax\\_liens'\n",
       "\\item 'public\\_record\\_bankrupt'\n",
       "\\item 'loan\\_purpose'\n",
       "\\item 'application\\_type'\n",
       "\\item 'loan\\_amount'\n",
       "\\item 'term'\n",
       "\\item 'interest\\_rate'\n",
       "\\item 'installment'\n",
       "\\item 'grade'\n",
       "\\item 'sub\\_grade'\n",
       "\\item 'issue\\_month'\n",
       "\\item 'loan\\_status'\n",
       "\\item 'initial\\_listing\\_status'\n",
       "\\item 'disbursement\\_method'\n",
       "\\item 'balance'\n",
       "\\item 'paid\\_total'\n",
       "\\item 'paid\\_principal'\n",
       "\\item 'paid\\_interest'\n",
       "\\item 'paid\\_late\\_fees'\n",
       "\\end{enumerate*}\n"
      ],
      "text/markdown": [
       "1. 'emp_title'\n",
       "2. 'emp_length'\n",
       "3. 'state'\n",
       "4. 'homeownership'\n",
       "5. 'annual_income'\n",
       "6. 'verified_income'\n",
       "7. 'debt_to_income'\n",
       "8. 'annual_income_joint'\n",
       "9. 'verification_income_joint'\n",
       "10. 'debt_to_income_joint'\n",
       "11. 'delinq_2y'\n",
       "12. 'months_since_last_delinq'\n",
       "13. 'earliest_credit_line'\n",
       "14. 'inquiries_last_12m'\n",
       "15. 'total_credit_lines'\n",
       "16. 'open_credit_lines'\n",
       "17. 'total_credit_limit'\n",
       "18. 'total_credit_utilized'\n",
       "19. 'num_collections_last_12m'\n",
       "20. 'num_historical_failed_to_pay'\n",
       "21. 'months_since_90d_late'\n",
       "22. 'current_accounts_delinq'\n",
       "23. 'total_collection_amount_ever'\n",
       "24. 'current_installment_accounts'\n",
       "25. 'accounts_opened_24m'\n",
       "26. 'months_since_last_credit_inquiry'\n",
       "27. 'num_satisfactory_accounts'\n",
       "28. 'num_accounts_120d_past_due'\n",
       "29. 'num_accounts_30d_past_due'\n",
       "30. 'num_active_debit_accounts'\n",
       "31. 'total_debit_limit'\n",
       "32. 'num_total_cc_accounts'\n",
       "33. 'num_open_cc_accounts'\n",
       "34. 'num_cc_carrying_balance'\n",
       "35. 'num_mort_accounts'\n",
       "36. 'account_never_delinq_percent'\n",
       "37. 'tax_liens'\n",
       "38. 'public_record_bankrupt'\n",
       "39. 'loan_purpose'\n",
       "40. 'application_type'\n",
       "41. 'loan_amount'\n",
       "42. 'term'\n",
       "43. 'interest_rate'\n",
       "44. 'installment'\n",
       "45. 'grade'\n",
       "46. 'sub_grade'\n",
       "47. 'issue_month'\n",
       "48. 'loan_status'\n",
       "49. 'initial_listing_status'\n",
       "50. 'disbursement_method'\n",
       "51. 'balance'\n",
       "52. 'paid_total'\n",
       "53. 'paid_principal'\n",
       "54. 'paid_interest'\n",
       "55. 'paid_late_fees'\n",
       "\n",
       "\n"
      ],
      "text/plain": [
       " [1] \"emp_title\"                        \"emp_length\"                      \n",
       " [3] \"state\"                            \"homeownership\"                   \n",
       " [5] \"annual_income\"                    \"verified_income\"                 \n",
       " [7] \"debt_to_income\"                   \"annual_income_joint\"             \n",
       " [9] \"verification_income_joint\"        \"debt_to_income_joint\"            \n",
       "[11] \"delinq_2y\"                        \"months_since_last_delinq\"        \n",
       "[13] \"earliest_credit_line\"             \"inquiries_last_12m\"              \n",
       "[15] \"total_credit_lines\"               \"open_credit_lines\"               \n",
       "[17] \"total_credit_limit\"               \"total_credit_utilized\"           \n",
       "[19] \"num_collections_last_12m\"         \"num_historical_failed_to_pay\"    \n",
       "[21] \"months_since_90d_late\"            \"current_accounts_delinq\"         \n",
       "[23] \"total_collection_amount_ever\"     \"current_installment_accounts\"    \n",
       "[25] \"accounts_opened_24m\"              \"months_since_last_credit_inquiry\"\n",
       "[27] \"num_satisfactory_accounts\"        \"num_accounts_120d_past_due\"      \n",
       "[29] \"num_accounts_30d_past_due\"        \"num_active_debit_accounts\"       \n",
       "[31] \"total_debit_limit\"                \"num_total_cc_accounts\"           \n",
       "[33] \"num_open_cc_accounts\"             \"num_cc_carrying_balance\"         \n",
       "[35] \"num_mort_accounts\"                \"account_never_delinq_percent\"    \n",
       "[37] \"tax_liens\"                        \"public_record_bankrupt\"          \n",
       "[39] \"loan_purpose\"                     \"application_type\"                \n",
       "[41] \"loan_amount\"                      \"term\"                            \n",
       "[43] \"interest_rate\"                    \"installment\"                     \n",
       "[45] \"grade\"                            \"sub_grade\"                       \n",
       "[47] \"issue_month\"                      \"loan_status\"                     \n",
       "[49] \"initial_listing_status\"           \"disbursement_method\"             \n",
       "[51] \"balance\"                          \"paid_total\"                      \n",
       "[53] \"paid_principal\"                   \"paid_interest\"                   \n",
       "[55] \"paid_late_fees\"                  "
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "colnames(DATA)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [],
   "source": [
    "DATU = na.omit(DATA[,c(\"loan_amount\",\"annual_income\",\"debt_to_income\",\"interest_rate\",\"total_credit_limit\")])\n",
    "\n",
    "COR_1= cor(DATU)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table>\n",
       "<caption>A xtable: 5 × 5</caption>\n",
       "<thead>\n",
       "\t<tr><th></th><th scope=col>loan_amount</th><th scope=col>annual_income</th><th scope=col>debt_to_income</th><th scope=col>interest_rate</th><th scope=col>total_credit_limit</th></tr>\n",
       "\t<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>\n",
       "</thead>\n",
       "<tbody>\n",
       "\t<tr><th scope=row>loan_amount</th><td>1.00000000</td><td> 0.32617701</td><td> 0.05632869</td><td> 0.06506083</td><td> 0.30404559</td></tr>\n",
       "\t<tr><th scope=row>annual_income</th><td>0.32617701</td><td> 1.00000000</td><td>-0.18044549</td><td>-0.09870405</td><td> 0.51705595</td></tr>\n",
       "\t<tr><th scope=row>debt_to_income</th><td>0.05632869</td><td>-0.18044549</td><td> 1.00000000</td><td> 0.14165342</td><td> 0.07517409</td></tr>\n",
       "\t<tr><th scope=row>interest_rate</th><td>0.06506083</td><td>-0.09870405</td><td> 0.14165342</td><td> 1.00000000</td><td>-0.12973379</td></tr>\n",
       "\t<tr><th scope=row>total_credit_limit</th><td>0.30404559</td><td> 0.51705595</td><td> 0.07517409</td><td>-0.12973379</td><td> 1.00000000</td></tr>\n",
       "</tbody>\n",
       "</table>\n"
      ],
      "text/latex": [
       "A xtable: 5 × 5\n",
       "\\begin{tabular}{r|lllll}\n",
       "  & loan\\_amount & annual\\_income & debt\\_to\\_income & interest\\_rate & total\\_credit\\_limit\\\\\n",
       "  & <dbl> & <dbl> & <dbl> & <dbl> & <dbl>\\\\\n",
       "\\hline\n",
       "\tloan\\_amount & 1.00000000 &  0.32617701 &  0.05632869 &  0.06506083 &  0.30404559\\\\\n",
       "\tannual\\_income & 0.32617701 &  1.00000000 & -0.18044549 & -0.09870405 &  0.51705595\\\\\n",
       "\tdebt\\_to\\_income & 0.05632869 & -0.18044549 &  1.00000000 &  0.14165342 &  0.07517409\\\\\n",
       "\tinterest\\_rate & 0.06506083 & -0.09870405 &  0.14165342 &  1.00000000 & -0.12973379\\\\\n",
       "\ttotal\\_credit\\_limit & 0.30404559 &  0.51705595 &  0.07517409 & -0.12973379 &  1.00000000\\\\\n",
       "\\end{tabular}\n"
      ],
      "text/markdown": [
       "\n",
       "A xtable: 5 × 5\n",
       "\n",
       "| <!--/--> | loan_amount &lt;dbl&gt; | annual_income &lt;dbl&gt; | debt_to_income &lt;dbl&gt; | interest_rate &lt;dbl&gt; | total_credit_limit &lt;dbl&gt; |\n",
       "|---|---|---|---|---|---|\n",
       "| loan_amount | 1.00000000 |  0.32617701 |  0.05632869 |  0.06506083 |  0.30404559 |\n",
       "| annual_income | 0.32617701 |  1.00000000 | -0.18044549 | -0.09870405 |  0.51705595 |\n",
       "| debt_to_income | 0.05632869 | -0.18044549 |  1.00000000 |  0.14165342 |  0.07517409 |\n",
       "| interest_rate | 0.06506083 | -0.09870405 |  0.14165342 |  1.00000000 | -0.12973379 |\n",
       "| total_credit_limit | 0.30404559 |  0.51705595 |  0.07517409 | -0.12973379 |  1.00000000 |\n",
       "\n"
      ],
      "text/plain": [
       "                   loan_amount annual_income debt_to_income interest_rate\n",
       "loan_amount        1.00000000   0.32617701    0.05632869     0.06506083  \n",
       "annual_income      0.32617701   1.00000000   -0.18044549    -0.09870405  \n",
       "debt_to_income     0.05632869  -0.18044549    1.00000000     0.14165342  \n",
       "interest_rate      0.06506083  -0.09870405    0.14165342     1.00000000  \n",
       "total_credit_limit 0.30404559   0.51705595    0.07517409    -0.12973379  \n",
       "                   total_credit_limit\n",
       "loan_amount         0.30404559       \n",
       "annual_income       0.51705595       \n",
       "debt_to_income      0.07517409       \n",
       "interest_rate      -0.12973379       \n",
       "total_credit_limit  1.00000000       "
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "xtable(COR_1)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### La correlacion mas fuerte con respecto a el valor del prestamo es el ingreso anual de la persona y el limite de dinero que la persona puede pedir prestada.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Punto 5:"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### El proceso para encontrar el algoritmo elegido, sera un auto machine learning proveniente de la libreria H2O, el cual hace una busqueda de grilla dentro de los modelos que la herramienta tiene disponible."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Para desarrollar el modelo es necesario, crear una caracteristica de tipo binaria, en donde 1 es igual a las siguientes categorias:\n",
    "- In Grace Period.\n",
    "- Late (31-120 days)\n",
    "- Late (16-30 days)\n",
    "\n",
    "####  0 las categorias restantes.\n",
    "#### El modelo escogido por el proceso de automachinelearning, fue un GLM ( Una regresion regularizada Ridge). Pues como muestra el proceso, es el algoritmo con el mejor performance."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "\n",
       "       Charged Off            Current         Fully Paid    In Grace Period \n",
       "                 7               9375                447                 67 \n",
       " Late (16-30 days) Late (31-120 days) \n",
       "                38                 66 "
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "table(DATA$loan_status)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {},
   "outputs": [],
   "source": [
    "DATA$BINARY_TARGET = ifelse(DATA$loan_status%in%c(\"In Grace Period\",\"Late (16-30 days)\",\"Late (31-120 days)\"),1,0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "\n",
      "H2O is not running yet, starting it now...\n",
      "\n",
      "Note:  In case of errors look at the following log files:\n",
      "    C:\\Users\\ASUS\\AppData\\Local\\Temp\\RtmpiOxJSM\\file35fc2f002500/h2o_ASUS_started_from_r.out\n",
      "    C:\\Users\\ASUS\\AppData\\Local\\Temp\\RtmpiOxJSM\\file35fc45a7324e/h2o_ASUS_started_from_r.err\n",
      "\n",
      "\n",
      "Starting H2O JVM and connecting: . Connection successful!\n",
      "\n",
      "R is connected to the H2O cluster: \n",
      "    H2O cluster uptime:         7 seconds 518 milliseconds \n",
      "    H2O cluster timezone:       America/Bogota \n",
      "    H2O data parsing timezone:  UTC \n",
      "    H2O cluster version:        3.30.0.1 \n",
      "    H2O cluster version age:    1 year, 7 months and 22 days !!! \n",
      "    H2O cluster name:           H2O_started_from_R_ASUS_bin226 \n",
      "    H2O cluster total nodes:    1 \n",
      "    H2O cluster total memory:   8.89 GB \n",
      "    H2O cluster total cores:    8 \n",
      "    H2O cluster allowed cores:  8 \n",
      "    H2O cluster healthy:        TRUE \n",
      "    H2O Connection ip:          localhost \n",
      "    H2O Connection port:        54321 \n",
      "    H2O Connection proxy:       NA \n",
      "    H2O Internal Security:      FALSE \n",
      "    H2O API Extensions:         Amazon S3, Algos, AutoML, Core V3, TargetEncoder, Core V4 \n",
      "    R Version:                  R version 3.6.1 (2019-07-05) \n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "Warning message in h2o.clusterInfo():\n",
      "\"\n",
      "Your H2O cluster version is too old (1 year, 7 months and 22 days)!\n",
      "Please download and install the latest version from http://h2o.ai/download/\""
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "\n"
     ]
    }
   ],
   "source": [
    "library(h2o)\n",
    "\n",
    "h2o.init(max_mem_size = \"10G\",nthreads=-1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "  |======================================================================| 100%\n"
     ]
    }
   ],
   "source": [
    "DATA_1 = as.h2o(DATA)\n",
    "DATA_1$BINARY_TARGET = as.factor(as.character(DATA_1$BINARY_TARGET))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "metadata": {},
   "outputs": [],
   "source": [
    "splits <- h2o.splitFrame(data=DATA_1, ratios=c(0.7))  \n",
    "train <- splits[[1]]\n",
    "test <- splits[[2]]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "  |                                                                      |   0%\n",
      "  |======================================================================| 100%\n"
     ]
    }
   ],
   "source": [
    "target <- \"BINARY_TARGET\"\n",
    "\n",
    "predictors <- c('emp_title','emp_length','state','homeownership','annual_income','debt_to_income',\n",
    "               'total_credit_lines','open_credit_lines','total_credit_limit','total_credit_utilized','current_installment_accounts'\n",
    "               ,'num_total_cc_accounts','num_open_cc_accounts','num_cc_carrying_balance','loan_purpose','loan_amount','term',\"interest_rate\"\n",
    "               )\n",
    "\n",
    "\n",
    "automl_h2o_models <- h2o.automl(\n",
    "  x = predictors, \n",
    "  y = target,\n",
    "  training_frame= train,  validation_frame = test,nfolds = 0,max_models=20, sort_metric = c(\"logloss\"),balance_classes = TRUE,exclude_algos=c(\"DeepLearning\",\"StackedEnsemble\"),seed=2020)\n",
    "\n",
    "lb <- h2o.get_leaderboard(automl_h2o_models)\n",
    "\n",
    "automl_leader <- automl_h2o_models@leader"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Model Details:\n",
       "==============\n",
       "\n",
       "H2OBinomialModel: glm\n",
       "Model ID:  GLM_1_AutoML_20211125_232545 \n",
       "GLM Model: summary\n",
       "    family  link              regularization\n",
       "1 binomial logit Ridge ( lambda = 0.002939 )\n",
       "                                                                lambda_search\n",
       "1 nlambda = 30, lambda.max = 1.2271, lambda.min = 0.002939, lambda.1se = -1.0\n",
       "  number_of_predictors_total number_of_active_predictors number_of_iterations\n",
       "1                       4821                        3317                   50\n",
       "                   training_frame\n",
       "1 automl_training_RTMP_sid_a96b_7\n",
       "\n",
       "Coefficients: glm coefficients\n",
       "                     names coefficients standardized_coefficients\n",
       "1                Intercept    -4.784576                 -4.035062\n",
       "2               emp_title.    -0.155757                 -0.155757\n",
       "3 emp_title.   maintenance    -0.001782                 -0.001782\n",
       "4         emp_title. admin     0.000000                  0.000000\n",
       "5 emp_title. combo psc/hub    -0.000674                 -0.000674\n",
       "\n",
       "---\n",
       "                       names coefficients standardized_coefficients\n",
       "4817   num_total_cc_accounts    -0.007186                 -0.057164\n",
       "4818    num_open_cc_accounts    -0.016895                 -0.083784\n",
       "4819 num_cc_carrying_balance     0.000089                  0.000302\n",
       "4820             loan_amount     0.000020                  0.202894\n",
       "4821                    term    -0.004217                 -0.046487\n",
       "4822           interest_rate     0.096381                  0.483473\n",
       "\n",
       "H2OBinomialMetrics: glm\n",
       "** Reported on training data. **\n",
       "\n",
       "MSE:  0.01791785\n",
       "RMSE:  0.1338576\n",
       "LogLoss:  0.0853161\n",
       "Mean Per-Class Error:  0.3848917\n",
       "AUC:  0.7442163\n",
       "AUCPR:  0.06652048\n",
       "Gini:  0.4884326\n",
       "R^2:  0.02101062\n",
       "Residual Deviance:  1079.59\n",
       "AIC:  7715.59\n",
       "\n",
       "Confusion Matrix (vertical: actual; across: predicted) for F1-optimal threshold:\n",
       "          0   1    Error       Rate\n",
       "0      5902 307 0.049444  =307/6209\n",
       "1        85  33 0.720339    =85/118\n",
       "Totals 5987 340 0.061957  =392/6327\n",
       "\n",
       "Maximum Metrics: Maximum metrics at their respective thresholds\n",
       "                        metric threshold       value idx\n",
       "1                       max f1  0.043626    0.144105 106\n",
       "2                       max f2  0.029012    0.215395 170\n",
       "3                 max f0point5  0.083032    0.149007  30\n",
       "4                 max accuracy  0.176713    0.981192   0\n",
       "5                max precision  0.140329    0.333333   2\n",
       "6                   max recall  0.005862    1.000000 375\n",
       "7              max specificity  0.176713    0.999839   0\n",
       "8             max absolute_mcc  0.029012    0.142292 170\n",
       "9   max min_per_class_accuracy  0.018773    0.662587 240\n",
       "10 max mean_per_class_accuracy  0.029012    0.687368 170\n",
       "11                     max tns  0.176713 6208.000000   0\n",
       "12                     max fns  0.176713  118.000000   0\n",
       "13                     max fps  0.001310 6209.000000 399\n",
       "14                     max tps  0.005862  118.000000 375\n",
       "15                     max tnr  0.176713    0.999839   0\n",
       "16                     max fnr  0.176713    1.000000   0\n",
       "17                     max fpr  0.001310    1.000000 399\n",
       "18                     max tpr  0.005862    1.000000 375\n",
       "\n",
       "Gains/Lift Table: Extract with `h2o.gainsLift(<model>, <data>)` or `h2o.gainsLift(<model>, valid=<T/F>, xval=<T/F>)`\n",
       "H2OBinomialMetrics: glm\n",
       "** Reported on validation data. **\n",
       "\n",
       "MSE:  0.0140614\n",
       "RMSE:  0.1185808\n",
       "LogLoss:  0.07158617\n",
       "Mean Per-Class Error:  0.4406457\n",
       "AUC:  0.7108307\n",
       "AUCPR:  0.05769214\n",
       "Gini:  0.4216615\n",
       "R^2:  0.01386064\n",
       "Residual Deviance:  425.5082\n",
       "AIC:  7061.508\n",
       "\n",
       "Confusion Matrix (vertical: actual; across: predicted) for F1-optimal threshold:\n",
       "          0  1    Error      Rate\n",
       "0      2868 61 0.020826  =61/2929\n",
       "1        37  6 0.860465    =37/43\n",
       "Totals 2905 67 0.032974  =98/2972\n",
       "\n",
       "Maximum Metrics: Maximum metrics at their respective thresholds\n",
       "                        metric threshold       value idx\n",
       "1                       max f1  0.057730    0.109091  47\n",
       "2                       max f2  0.041696    0.159884  92\n",
       "3                 max f0point5  0.108585    0.158730   3\n",
       "4                 max accuracy  0.137656    0.985532   0\n",
       "5                max precision  0.137656    0.500000   0\n",
       "6                   max recall  0.008178    1.000000 352\n",
       "7              max specificity  0.137656    0.999659   0\n",
       "8             max absolute_mcc  0.108585    0.132538   3\n",
       "9   max min_per_class_accuracy  0.018678    0.648003 230\n",
       "10 max mean_per_class_accuracy  0.022693    0.670008 196\n",
       "11                     max tns  0.137656 2928.000000   0\n",
       "12                     max fns  0.137656   42.000000   0\n",
       "13                     max fps  0.000184 2929.000000 399\n",
       "14                     max tps  0.008178   43.000000 352\n",
       "15                     max tnr  0.137656    0.999659   0\n",
       "16                     max fnr  0.137656    0.976744   0\n",
       "17                     max fpr  0.000184    1.000000 399\n",
       "18                     max tpr  0.008178    1.000000 352\n",
       "\n",
       "Gains/Lift Table: Extract with `h2o.gainsLift(<model>, <data>)` or `h2o.gainsLift(<model>, valid=<T/F>, xval=<T/F>)`\n"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "automl_leader"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "                                     model_id    logloss       auc      aucpr\n",
       "1                GLM_1_AutoML_20211125_232545 0.06603403 0.8479016 0.08913379\n",
       "2  GBM_grid__1_AutoML_20211125_232545_model_7 0.08422648 0.6384949 0.02294432\n",
       "3 GBM_grid__1_AutoML_20211125_232545_model_12 0.08688819 0.4183068 0.01285106\n",
       "4  GBM_grid__1_AutoML_20211125_232545_model_9 0.09039799 0.4801737 0.01311696\n",
       "5                GBM_1_AutoML_20211125_232545 0.09117728 0.4693198 0.01341585\n",
       "6  GBM_grid__1_AutoML_20211125_232545_model_6 0.09132504 0.4188857 0.01198474\n",
       "  mean_per_class_error      rmse        mse\n",
       "1            0.4043415 0.1168171 0.01364623\n",
       "2            0.4188133 0.1190367 0.01416973\n",
       "3            0.4659190 0.1191969 0.01420791\n",
       "4            0.4854559 0.1192764 0.01422686\n",
       "5            0.4702605 0.1194501 0.01426833\n",
       "6            0.4724313 0.1193545 0.01424550\n",
       "\n",
       "[20 rows x 7 columns] "
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "lb"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "##### Performance en Test dataframe:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[1] 0.7108307\n"
     ]
    }
   ],
   "source": [
    "print(h2o.auc(automl_leader, valid = TRUE))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Lo interesante de los algoritmos GLM regularizados es que no sufren de sobreajuste por esta razon, los resultados de este modelo en entrenamiento pueden ser considerados confiables para un entorno de produccion."
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "R",
   "language": "R",
   "name": "ir"
  },
  "language_info": {
   "codemirror_mode": "r",
   "file_extension": ".r",
   "mimetype": "text/x-r-source",
   "name": "R",
   "pygments_lexer": "r",
   "version": "3.6.1"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
