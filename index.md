<style type='text/css'> 

    .embeddedServiceHelpButton .helpButton .uiButton { 

        background-color: #0e2152; 

        font-family: "Arial", sans-serif; 

    } 

    .embeddedServiceHelpButton .helpButton .uiButton:focus { 

        outline: 1px solid #0e2152; 

    } 

</style> 

 

<script type='text/javascript' src='https://service.force.com/embeddedservice/5.0/esw.min.js'></script> 

<script type='text/javascript'> 

    var initESW = function(gslbBaseURL) { 

        embedded_svc.settings.displayHelpButton = true; // Or false 

        embedded_svc.settings.language = ''; // For example, enter 'en' or 'en-US' 

 

        embedded_svc.settings.enabledFeatures = ['LiveAgent']; 

        embedded_svc.settings.entryFeature = 'LiveAgent'; 

 

        // Add direct-to-button routing based on pre-chat form responses 

        embedded_svc.settings.directToButtonRouting = function(prechatFormData) { 

            console.log(prechatFormData); 

            // Iterate through pre-chat form data to find the 'What_can_we_assist_with__c' field 

        console.log('In logic section'); 

            console.log(prechatFormData[7].value); 

            if (prechatFormData[7].value === 'Agency ID/Member ID' || prechatFormData[7].value === 'CDE hours' || prechatFormData[7].value === 'Recertification') { 

                console.log('Routing to new queue'); 

                return '573Ro0000000Ue1'; 

            } 

        }; 

 

        embedded_svc.settings.extraPrechatFormDetails = [{"label":"What can we assist with?", "transcriptFields": ["Request_Reason__c"]}, {"label":"First Name", "transcriptFields": ["Visitor_First_Name__c"]},{"label":"Last Name", "transcriptFields": ["Visitor_Last_Name__c"]},{"label":"Phone", "transcriptFields": ["Phone__c"]},{"label":"Email", "transcriptFields": ["Email__c"]}]; 

         

        embedded_svc.init( 

            'https://prioritypdc.my.salesforce.com', 

            'https://prioritypdc.my.salesforce-sites.com/digengage', 

            gslbBaseURL, 

            '00D610000006NpG', 

            'Course_Coordination', 

            { 

                baseLiveAgentContentURL: 'https://c.la1-core1.sfdc-lywfpd.salesforceliveagent.com/content', 

                deploymentId: '5724N000000GyED', 

                buttonId: '5734N000000GzEV', 

                baseLiveAgentURL: 'https://d.la1-core1.sfdc-lywfpd.salesforceliveagent.com/chat', 

                eswLiveAgentDevName: 'EmbeddedServiceLiveAgent_Parent04I4N000000KynhUAC_17ec0e19017', 

                isOfflineSupportEnabled: true 

            } 

        ); 

    }; 

 

    if (!window.embedded_svc) { 

        var s = document.createElement('script'); 

        s.setAttribute('src', 'https://prioritypdc.my.salesforce.com/embeddedservice/5.0/esw.min.js'); 

        s.onload = function() { 

            initESW(null); 

        }; 

        document.body.appendChild(s); 

    } else { 

        initESW('https://service.force.com'); 

    } 

</script>
