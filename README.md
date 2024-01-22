   # Mamdani Fuzzy Inference System for Heart Attack Risk Detection
   #### Video Demo:  <URL https://youtu.be/2Ejxz3uulF0>
   #### Description:

In this work, I will focus on the issue of predicting heart attacks using a Mandani fuzzy system programmed in the Python programming language. Within our system, we primarily obtain input values from the patient, representing key parameters such as age, BMI, blood pressure, and cholesterol level. These values are then processed using a fuzzy logic model, which utilizes membership functions from the SKfuzzy library to define fuzzy sets for different categories, such as age groups, weight indexes, and levels of risk factors. The model further uses a system of fuzzy rules to combine the fuzzy values of inputs and predict the risk of a heart attack.
The entire process includes fuzzification of inputs, setting rules, combining and evaluating results, and finally defuzzification to obtain a specific output value, i.e., a percentage expression of the risk level of a heart attack. Fuzzy logic, with its ability to model uncertainty, provides a flexible framework for risk analysis in this project.



<div style="text-align: justify; text-justify: distribute;">


**1. Defining Variables and importing necessary libraries**

Initially, we attempted to create and compute a fuzzy logic model based on specified values such as age, BMI, blood pressure, and cholesterol level. To create this model, in the first step, we import the Skfuzzy library for manipulating fuzzy sets and corresponding operations, as well as other necessary libraries for data manipulation.

**2. Geting and testing input**

This step involves prompting the user for their health metrics, ensuring that the values provided are positive, and verifying that they fall within realistic and acceptable ranges. If the inputted values are either non-positive or exceed predefined maximum limits, the program raises errors to alert the user of the incorrect input. This system is designed to ensure that the health data entered is both valid and within a reasonable scope for further processing or analysis.


**3. Creation of Fuzzy Sets, Definition of Membership Function, Fuzzification of Variables**

In the next step, I defined fuzzy sets for the input variables (age, BMI, blood pressure, and cholesterol level), which are relevant for predicting heart attacks. To accurately and adequately define these sets, I determined their endpoints based on expert sites (https://ruvzpb.szm.com/rizika.html, https://www.benulekaren.sk/cholesterol-zdrava-hladina-a-preco-znizovat-cholesterol-v-krvi).
Subsequently, I used the trapmf. function from the Skfuzzy library, which defines a membership function using four values to create a trapezoidal shape. This step ensured the representation of young, middle-aged, and old age groups, normal weight, overweight, and obesity BMI, low, medium, high, and very high blood pressure, and low, medium, and high cholesterol levels. Finally, I defined fuzzy sets for the output variable - the risk of a heart attack.

Further in the model, I endeavored to assign the membership of input values to the respective fuzzy sets defined by the trapezoidal membership function. Specifically, I use the fuzz.interp_membership function, which generates membership values for each input variable in relation to the respective fuzzy sets (e.g., young, middle-aged, old age).

**4. Creation of a Rule System**

Subsequently, I attempted to create a rule system that combines input variables and forms rules for predicting the risk of a heart attack. These rules are created based on the combination of membership values of the input variables defined in fuzzy sets. It's important to emphasize that these rules represent only the combinations of selected cases I have created, and as I am not a professional in the field of healthcare, and there is no scope in this project to create all possible combinations of variables, I selected 16 rules that, in my opinion, best demonstrate the correct and efficient functioning of this model. I create rules in the system using the "IF – THEN" approach, utilizing the t-compositional rule of inference for t* = tm, which is known as Mamdani's method.

**5. Combining Sets and Defuzzification**

Since my model is based on inference with multiple variables at the input and multiple rules, we need to consider the shape of this structure. In such a case, we combine individual rules disjunctively. By applying Mamdani's method and the maximum t-conorm for disjunction, we get an inference which in our project looks as follows:

    def agregation(pravidlo1,pravidlo2,pravidlo3,pravidlo4,pravidlo5,pravidlo6,pravidlo7,pravidlo8,pravidlo9,pravidlo10,pravidlo11,pravidlo12,pravidlo13,pravidlo14,pravidlo15,pravidlo16):
        out_nie = np.fmax(pravidlo1, pravidlo2)
        out_male = np.fmax(pravidlo15, pravidlo16)
        out_stredne = np.fmax(np.fmax(np.fmax(np.fmax(pravidlo3, pravidlo4),pravidlo5),pravidlo6), pravidlo7)
        out_vysoke = np.fmax(np.fmax(np.fmax(np.fmax(pravidlo8, pravidlo9), pravidlo10), pravidlo11), pravidlo12)
        out_velmi_vysoke = np.fmax(pravidlo13, pravidlo14)
        # Agregácia výstupov (max)
        aggregated = np.fmax(np.fmax(np.fmax(out_nie, out_male), out_stredne), np.fmax(out_vysoke, out_velmi_vysoke))

        return aggregated


Since our model represents a Mandani fuzzy system, in order to obtain a specific output value, i.e., a percentage expression of the risk level of a heart attack, we must perform defuzzification. For defuzzification, we choose the defuzzy function from the Skfuzzy library, which returns a defuzzified output value for the membership function mf using a specified defuzzification method. I chose the centroid method, which is the area's center of gravity, as my method of defuzzification."


**6. Application of the Model – Specific Cases**

+   *case 1* - We will test the functioning of the model on two specific cases. In the first example, we have a patient with ideal health predispositions. Patient No. 1 is 23 years old, has a BMI of 19, a systolic blood pressure of 110, and a cholesterol level of 4 mmol/l. The patient initially enters their health data. The result of the model - the model predicts only a *9%* risk of heart disease for the patient, and this result falls within the *'no risk' set*.
+   *case 2* - We have a patient who is 70 years old, with a BMI of 35, a systolic blood pressure of 200, and a cholesterol level of 7 mmol/l. In this case, the model predicted an *87%* risk of heart disease for the patient, and their result falls within the fuzzy set of *'Very High Risk*.

**Conclusion**

In this project, I attempted to create a fuzzy logic model for predicting the risk of a heart attack. I started by defining input variables such as age, BMI, blood pressure, and cholesterol level. Then, I created fuzzy sets for these variables using trapezoidal membership functions and the trapmf functions from the Skfuzzy library. Next, I assigned membership values to the respective fuzzy sets for each input variable. I created 16 rules for combining the input values and defined fuzzy sets. By combining individual rules, I created an inference structure and finally performed defuzzification using the centroid method, which is the area's center of gravity. In conclusion, I verified the functionality of this model by applying it to specific examples of patients with various input values.


<br></br>



</div>
<div style="text-align: right">
Written by Diana Sablicova<br>
On 17.01.2024
</div>