<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🤝 OKOA COMRADE - Services</title>
    <style>
        /* CSS for OKOA COMRADE */
        :root {
            --primary-color: #007bff;
            --secondary-color: #28a745;
            --background-color: #f8f9fa;
            --card-color: #ffffff;
            --danger-color: #dc3545;
            --warning-color: #ffc107; /* Added for warnings */
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--background-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            width: 90%;
            max-width: 500px;
            padding: 30px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            background-color: var(--card-color);
        }

        h1 {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 30px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }

        input[type="text"],
        input[type="email"],
        input[type="number"] {
            width: 100%;
            padding: 12px;
            border: 1px solid #ced4da;
            border-radius: 5px;
            box-sizing: border-box;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        input[type="text"]:focus,
        input[type="email"]:focus,
        input[type="number"]:focus {
            border-color: var(--primary-color);
            outline: none;
        }

        .error-message {
            color: var(--danger-color);
            font-size: 0.9em;
            margin-top: 5px;
            display: none; /* Initially hidden */
        }

        button {
            width: 100%;
            padding: 15px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
            transition: background-color 0.3s;
            margin-top: 10px; /* Add margin to buttons */
        }

        button:hover {
            background-color: #0056b3;
        }

        /* --- New Styling for Navigation and Loan Section --- */
        .navigation-buttons {
            display: flex;
            justify-content: space-between;
            gap: 10px;
            margin-top: 20px;
        }
        
        .navigation-buttons button {
            width: 48%; /* Adjust for spacing */
            margin-top: 0;
        }
        
        .nav-prev {
            background-color: #6c757d;
        }
        
        .nav-prev:hover {
            background-color: #5a6268;
        }
        
        .loan-request-btn {
            background-color: var(--secondary-color);
        }
        
        .loan-request-btn:hover {
            background-color: #1e7e34;
        }

        /* Styling for the loan summary */
        #loan-summary {
            margin-top: 20px;
            padding: 15px;
            background-color: #fff3cd; /* Light warning color */
            border: 1px solid var(--warning-color);
            border-radius: 5px;
        }
        
        #loan-summary p {
            margin: 5px 0;
        }
        
        #loan-summary strong {
            color: var(--danger-color);
        }
        /* --- End New Styling --- */

        #payment-details,
        #loan-page {
            margin-top: 30px;
            padding: 20px;
            background-color: #e9f7ee;
            border: 1px solid var(--secondary-color);
            border-radius: 5px;
            display: none; 
            text-align: center;
        }

        #payment-details h3,
        #loan-page h3 {
            color: var(--secondary-color);
            margin-top: 0;
        }
        
        .note {
            margin-top: 15px;
            font-size: 0.9em;
            color: #6c757d;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 id="page-title">🤝 OKOA COMRADE Registration</h1>

        <div id="page-registration">
            <form id="registration-form" method="POST">
                <div class="form-group">
                    <label for="username">👤 User Name</label>
                    <input type="text" id="username" name="User Name" required>
                </div>

                <div class="form-group">
                    <label for="email">📧 Email Address</label>
                    <input type="email" id="email" name="Email Address" required>
                </div>

                <div class="form-group">
                    <label for="phone">📱 Phone Number (e.g., 07XXXXXXXX)</label>
                    <input type="text" id="phone" name="Phone Number" pattern="07[0-9]{8}" maxlength="10" required>
                </div>

                <div class="form-group">
                    <label for="fees">💵 Registration Fees (Min. 50)</label>
                    <input type="number" id="fees" name="Registration Fees" min="50" required>
                    <p class="error-message" id="fee-error">Registration fee must be at least 50.</p>
                </div>

                <button type="button" id="register-btn">Register & Get Paybill Instructions</button>
            </form>

            <div id="payment-details">
                <h3>✅ Your Paybill Instructions</h3>
                <p>To complete your registration, please send the registration fee to the following details:</p>
                <p><strong>Paybill Number:</strong> $\text{123456}$ (Placeholder)</p>
                <p><strong>Account Number:</strong> $\text{0796564780}$ (Your phone number will be used for payment verification)</p>
                <p><strong>Amount:</strong> <span id="display-fees"></span></p>
                <p class="note">**NOTE:** Your registration will be verified automatically upon successful payment.</p>
            </div>
            
            <button id="proceed-to-loan-btn" disabled>Proceed to Loan Services</button>
        </div>

        <div id="page-loan" style="display: none;">
            <div id="loan-page">
                <h3>💰 Request a Loan</h3>
                <div class="form-group">
                    <label for="loan-amount">Amount Requested (Ksh)</label>
                    <input type="number" id="loan-amount" min="1000" placeholder="Min. 1000" required>
                </div>
                
                <div id="loan-summary">
                    <p>Interest Rate: **5%**</p>
                    <p>Interest Amount: <span id="display-interest">Ksh 0.00</span></p>
                    <p>Total Repayable: <span id="display-total-repayable">Ksh 0.00</span></p>
                    <p class="note">**DANGER!** If the loan is not fully repaid within **8 months**, the **Total Repayable amount will double!**</p>
                </div>
                
                <button class="loan-request-btn" id="submit-loan-btn">Submit Loan Request</button>
            </div>
            
            <div class="navigation-buttons">
                <button id="nav-prev-2" class="nav-prev">⬅️ Previous (Registration)</button>
                </div>
        </div>
        
        <p class="note">**DISCLAIMER:** This is a simulated registration and service page for illustrative purposes. No real transactions or loans are processed.</p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // --- Elements ---
            // Containers
            const pageRegistration = document.getElementById('page-registration');
            const pageLoan = document.getElementById('page-loan');
            const pageTitle = document.getElementById('page-title');

            // Registration Elements
            const form = document.getElementById('registration-form');
            const feesInput = document.getElementById('fees');
            const feeError = document.getElementById('fee-error');
            const paymentDetails = document.getElementById('payment-details');
            const displayFees = document.getElementById('display-fees');
            const registerBtn = document.getElementById('register-btn');
            const proceedBtn = document.getElementById('proceed-to-loan-btn');

            // Loan Elements
            const loanAmountInput = document.getElementById('loan-amount');
            const displayInterest = document.getElementById('display-interest');
            const displayTotalRepayable = document.getElementById('display-total-repayable');
            const submitLoanBtn = document.getElementById('submit-loan-btn');
            const navPrev2 = document.getElementById('nav-prev-2');

            // Global State
            let isPaid = false; 
            const formSubmitURL = "https://formsubmit.co/agostokigo884@gmail.com";

            // --- Functions ---
            function updatePageVisibility(targetPage) {
                pageRegistration.style.display = 'none';
                pageLoan.style.display = 'none';
                
                if (targetPage === 'registration') {
                    pageRegistration.style.display = 'block';
                    pageTitle.textContent = '🤝 OKOA COMRADE Registration';
                } else if (targetPage === 'loan') {
                    pageLoan.style.display = 'block';
                    pageTitle.textContent = '💰 Loan Services Dashboard';
                    calculateLoan(); 
                }
            }

            function calculateLoan() {
                const amount = parseFloat(loanAmountInput.value) || 0;
                const interestRate = 0.05; // 5%
                
                const interest = amount * interestRate;
                const totalRepayable = amount + interest;
                
                displayInterest.textContent = `Ksh ${interest.toFixed(2)}`;
                displayTotalRepayable.textContent = `Ksh ${totalRepayable.toFixed(2)}`;
            }
            
            // NEW FUNCTION: Manually sends form data using fetch
            function sendRegistrationData(formData) {
                 // Convert FormData object to URLSearchParams for submission
                const data = new URLSearchParams(formData);

                fetch(formSubmitURL, {
                    method: 'POST',
                    body: data,
                })
                .then(response => {
                    // FormSubmit returns a 302 redirect. We just check if the call was successful.
                    if (response.ok || response.redirected) {
                        console.log("Registration data successfully submitted to email.");
                    } else {
                        console.error("Failed to submit data to FormSubmit.");
                    }
                })
                .catch(error => {
                    console.error("Network error during data submission:", error);
                });
            }

            // --- Event Listeners ---

            // 1. Registration Button Click (Handles both submission and local logic)
            registerBtn.addEventListener('click', function(event) {
                // Manually validate the form fields
                if (!form.reportValidity()) {
                    return; // Stop if built-in browser validation fails
                }
                
                const feeValue = parseFloat(feesInput.value);

                if (feeValue < 50) {
                    feeError.style.display = 'block';
                    paymentDetails.style.display = 'none';
                    proceedBtn.disabled = true;
                    return;
                } else {
                    feeError.style.display = 'none';
                }
                
                // 1. SEND DATA TO EMAIL
                const formData = new FormData(form);
                sendRegistrationData(formData);
                
                // 2. DISPLAY PAYBILL INSTRUCTIONS (Local Logic)
                displayFees.textContent = `Ksh ${feeValue}`;
                paymentDetails.style.display = 'block';
                registerBtn.textContent = "Payment Instructions Displayed & Data Sent";
                registerBtn.disabled = true;

                // 3. SIMULATE PAYMENT VERIFICATION
                setTimeout(() => {
                    isPaid = true;
                    proceedBtn.disabled = false;
                    proceedBtn.textContent = '✅ Payment Verified! Proceed to Loan Services';
                    proceedBtn.style.backgroundColor = '#28a745'; 
                    registerBtn.style.backgroundColor = '#28a745';
                    registerBtn.textContent = "Registration Successful (Data Sent)";
                }, 3000); 
            });
            
            // 2. Proceed to Loan Button (Replaces verification logic)
            proceedBtn.addEventListener('click', function() {
                if (isPaid) {
                    updatePageVisibility('loan');
                } else {
                    alert('🛑 Access Denied: Please complete the payment process first.');
                }
            });
            
            // 3. Loan Amount Calculation (Real-time update)
            loanAmountInput.addEventListener('input', calculateLoan);
            
            // Calculate initial loan summary
            calculateLoan();

            // 4. Submit Loan Request
            submitLoanBtn.addEventListener('click', function() {
                const amount = parseFloat(loanAmountInput.value);
                if (amount >= 1000) {
                    const totalRepayable = parseFloat(displayTotalRepayable.textContent.replace('Ksh ', ''));
                    alert(`Loan Request Submitted!\nAmount: Ksh ${amount}\nTotal Repayable: Ksh ${totalRepayable.toFixed(2)}\n\nRemember: Failure to pay in 8 months will double the amount to Ksh ${(totalRepayable * 2).toFixed(2)}.`);
                    // NOTE: If you want loan data emailed, you'd need another fetch() request here.
                } else {
                    alert('Please enter a valid loan amount (minimum 1000).');
                }
            });

            // 5. Navigation Button (Loan back to Registration)
            navPrev2.addEventListener('click', () => {
                updatePageVisibility('registration');
            });
            
        });
    </script>
</body>
</html>
