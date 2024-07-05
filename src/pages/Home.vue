<template>
    <div class="w-full mt-20">
        <div class="flex justify-center">
            <div class="card w-[1100px] bg-base-100 shadow-xl">
                <v-form :validation-schema="schema" @submit="onSubmit">
                    <!-- Input Field -->
                    <div class="flex ml-8">
                        <div>
                            <Field label="Name" type="text" holder="John Doe" v-model="nameField" class="mb-3"
                                @click="validateName" @keyup="validateNameField"
                                :class="{ 'input-danger': nameRequireError }" />
                            <span v-if="nameRequireError" class="text-xs text-red-600 ml-2"> Name is a required field
                            </span>
                            <span v-if="nameLenError" class="text-xs text-red-600 ml-2">
                                Name should be more than 2 and less than 20 characters
                            </span>
                        </div>

                        <div class="mx-10">
                            <Field label="Email" type="text" holder="johndoe@gmail.com" v-model="emailField"
                                class="mb-3" @keyup="validateEmailField" />
                            <span v-if="emailRequireError" class="text-xs text-red-600 ml-2">
                                Email is a required field
                            </span>
                            <span v-if="emailInvalidError" class="text-xs text-red-600 ml-2">
                                Email is invalid
                            </span>
                        </div>

                        <div>
                            <Field label="Mobile No." type="text" holder="(844) 233 - 9999" v-model="mobileField"
                                class="mb-3" maxlength="10" @input="formatMobileNoField" @keypress="isNumber"
                                @keyup="validateMobileNoField" />
                            <span v-if="mobileNoRequireError" class="text-xs text-red-600 ml-2">
                                Mobile No is a required field
                            </span>
                            <span v-if="mobileNoLenError" class="text-xs text-red-600 ml-2">
                                Please enter minimum 10 digits
                            </span>
                        </div>
                    </div>

                    <div class="flex ml-8">
                        <!-- DOB -->
                        <div class="flex justify-left">
                            <div>
                                <label class="label">
                                    <span class="font-semibold text-slate-600 label-text">Date of Birth : </span>
                                </label>
                                <input type="date" v-model="birthDate" class="btn w-80" required>
                            </div>
                        </div>

                        <!-- Gender Radio Buttons -->
                        <div class="flex justify-left items-center mx-10">
                            <div>
                                <label class="label">
                                    <span class="font-semibold text-slate-600 label-text">Gender : </span>
                                </label>
                                <div class="btn w-80">
                                    <span class="label-text ml-2">Male</span>
                                    <input value="Male" type="radio" name="radio-1" class="radio ml-2"
                                        v-model="genderRadio" />
                                    <span class="label-text ml-2">Female</span>
                                    <input value="Female" type="radio" name="radio-1" class="radio ml-2"
                                        v-model="genderRadio" />
                                    <span class="label-text ml-2">Others</span>
                                    <input value="Others" type="radio" name="radio-1" class="radio ml-2"
                                        v-model="genderRadio" />
                                    <!-- <Radio label="Male" value="Male" name="genderRadio" v-model="genderRadio" />
                                    <Radio label="Female" value="Female" name="genderRadio" v-model="genderRadio" />
                                    <Radio label="Others" value="Others" name="genderRadio" v-model="genderRadio" /> -->
                                </div>
                            </div>
                        </div>

                        <!-- Language Check Boxes -->
                        <div class="flex justify-left">
                            <div>
                                <label class="label">
                                    <span class="font-semibold text-slate-600 label-text">Language : </span>
                                </label>
                                <div class="btn w-80">
                                    <span class="label-text ml-2">Vue</span>
                                    <input value="Vue" type="checkbox" v-model="languageSelected"
                                        class="checkbox ml-2" />
                                    <span class="label-text ml-2">Angular</span>
                                    <input value="Angular" type="checkbox" v-model="languageSelected"
                                        class="checkbox ml-2" />
                                    <span class="label-text ml-2">React</span>
                                    <input value="React" type="checkbox" v-model="languageSelected"
                                        class="checkbox ml-2" />
                                    <!-- <CheckBox label="Vue" value="vue" v-model="languageSelected" />
                                    <CheckBox label="Angular" value="angular" v-model="languageSelected" />
                                    <CheckBox label="React" value="react" v-model="languageSelected" /> -->
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="flex justify-center">
                        <!-- City Dropdown -->
                        <div class="flex justify-left ml-8 items-center">
                            <div>
                                <label class="label">
                                    <span class="font-semibold text-slate-600 label-text">City : </span>
                                </label>
                                <select class="select select-bordered w-80" v-model="selectedCity">
                                    <option disabled selected value="">Select City</option>
                                    <option v-for="city in cities" :value="city">{{ city }}</option>
                                </select>
                            </div>
                        </div>

                        <!-- File Uploader -->
                        <div class="flex justify-center ml-10">
                            <div>
                                <div>
                                    <label class="label">
                                        <span class="font-semibold text-slate-600 label-text">File Upload : </span>
                                    </label>
                                    <input v-on="file" type="file" class="file-input w-full max-w-xs"
                                        accept=".jpg,.jpeg,application/pdf" @change="ValidateFile($event)" />
                                </div>
                                <span v-if="fileError" class="text-xs text-red-600 ml-2">
                                    File type not supported
                                </span>
                            </div>
                        </div>
                    </div>

                    <!-- Form Submitting Button -->
                    <div class="flex justify-center my-5">
                        <button :disabled="isSubmitting" @click="handleSubmit"
                            class="btn btn-outline btn-wide">Submit</button>
                    </div>
                </v-form>
            </div>
        </div>
    </div>

    <div>
        <div class="overflow-formattingMobileNoField-auto">
            <table class="table">
                <thead>
                    <tr>
                        <th></th>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Mobile No.</th>
                        <th>DOB</th>
                        <th>Gender</th>
                        <th>Languages</th>
                        <th>City</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(data, index) in formData">
                        <td>{{ index + 1 }}</td>
                        <td>{{ data.nameField }}</td>
                        <td>{{ data.emailField }}</td>
                        <td>{{ data.mobileField }}</td>
                        <td>{{ data.formatBirthDate ? formatBirthDate(data.formatBirthDate) : '---' }}</td>
                        <td>{{ data.genderRadio ? data.genderRadio : '---' }}</td>
                        <td>
                            <ul v-if="data.languageSelected.length">
                                <li v-for="lang in data.languageSelected"> {{ lang }}</li>
                            </ul>
                            <span v-else>---</span>
                        </td>
                        <td>{{ data.selectedCity ? data.selectedCity : '---' }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";

import Field from "../components/Field.vue";
// import Radio from "../components/Radio.vue";
// import CheckBox from "../components/CheckBox.vue";
import Select from "../components/Select.vue";
import { cities } from "../utils/Cities"
import moment from "moment";

const nameField = ref("");
const emailField = ref("");
const mobileField = ref("");
const birthDate = ref("");
const genderRadio = ref("");
const languageSelected = ref([])
const selectedCity = ref("");

const nameLenError = ref(false)
const nameRequireError = ref(false)

const emailRequireError = ref(false)
const emailInvalidError = ref(false)

const mobileNoLenError = ref(false)
const mobileNoRequireError = ref(false)

const fileError = ref(false)
const formData = ref([])

function validateNameField() {
    if (!nameField.value) {
        nameRequireError.value = true
        nameLenError.value = false
    } else {
        nameRequireError.value = false
        if (nameField.value.length <= 2 || nameField.value.length >= 20) {
            nameLenError.value = true
        } else {
            nameLenError.value = false
        }
    }
}

function validateEmailField() {
    if (!emailField.value) {
        emailRequireError.value = true
        emailInvalidError.value = false
    } else {
        emailRequireError.value = false
        if (emailField.value) {
            const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
            if (emailRegex.test(emailField.value.toLocaleLowerCase()) == false) {
                emailInvalidError.value = true
            } else {
                emailInvalidError.value = false
            }
        } else {
            emailRequireError.value = false
        }
    }
}

function validateMobileNoField() {
    if (!mobileField.value) {
        mobileNoRequireError.value = true
        mobileNoLenError.value = false
    } else {
        mobileNoRequireError.value = false
        if (mobileField.value.length >= 14) {
            mobileNoLenError.value = false
        } else {
            mobileNoLenError.value = true
        }
    }
}

function formatMobileNoField($event) {
    let formattingMobileNoField = mobileField.value.replace(/\D/g, '');
    let formattedMobileField = '';

    if (formattingMobileNoField.length > 0) {
        formattedMobileField += '(' + formattingMobileNoField.substring(0, 3);
    }
    if (formattingMobileNoField.length >= 4) {
        formattedMobileField += ') ' + formattingMobileNoField.substring(3, 6);
    }
    if (formattingMobileNoField.length >= 7) {
        formattedMobileField += '-' + formattingMobileNoField.substring(6, 10);
    }
    event.target.value = formattedMobileField;
};

function formatMobileNo(mobileField) {
    const cleaned = ('' + mobileField).replace(/\D/g, '');
    const match = cleaned.match(/^(\d{3})(\d{3})(\d{4})$/);
    if (match) {
        return '(' + match[1] + ') ' + match[2] + '-' + match[3];
    }
    return null;
}

function isNumber($event) {
    const keyCode = ($event.keyCode ? $event.keyCode : $event.which);
    if (keyCode < 48 || keyCode > 57) {
        $event.preventDefault();
    }
}

function formatBirthDate(birthDate) {
    return moment(birthDate).format('ll')
};

function ValidateFile(event) {
    const { target } = event;
    if (!['jpeg', 'jpg', 'pdf'].includes(target.value.split('.')[1])) {
        event.target.value = null;
        fileError.value = true
    } else {
        fileError.value = false
    }
}

function handleSubmit() {
    validateNameField()
    validateEmailField()
    validateMobileNoField()
    if (
        nameLenError.value == true ||
        emailRequireError.value == true ||
        mobileNoLenError.value == true ||
        emailRequireError.value == true ||
        emailInvalidError.value == true
    ) {
        return
    } else {
        formData.value.push({
            nameField: nameField.value,
            emailField: emailField.value,
            mobileField: mobileField.value,
            formatBirthDate: birthDate.value,
            genderRadio: genderRadio.value,
            languageSelected: languageSelected.value,
            selectedCity: selectedCity.value
        })
    }
    nameField.value = "",
        emailField.value = "",
        mobileField.value = "",
        birthDate.value = "",
        genderRadio.value = "",
        languageSelected.value = [],
        selectedCity.value = ""
}
</script>