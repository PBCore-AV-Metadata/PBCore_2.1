# PBCore_2.1
Update to the Public Broadcasting Metadata Dictionary project

After a long process of review, we are excited to announce the updated PBCore 2.1 schema! 

In deciding what changes to implement for PBCore 2.1, the PBCore Schema Team considered the following criteria:

What problems and challenges with the PBCore 2.0 schema were brought up during our open call for PBCore users to submit issues on GitHub as of September 30, 2014? </br>
What issues required a change to the schema, and what issues could be resolved by improving the documentation around PBCore elements and attributes to clarify their usage? </br>
What changes would allow the 2.1 schema to remain backwards compatible with PBCore 2.0, so that current users could continue to validate their metadata? Keep in mind that PBCore 2.1 is an incremental version, not a major release.

After balancing these considerations, we decided to implement the following schema changes for PBCore 2.1:

In 2.0, the collection of attributes that includes ‘@source, @ref, @version, @annotation’ -- which is designed to allow catalogers to provide accurate information about the source of their metadata -- was available to most elements, but not all of them. 

The updated schema provides the option to include ‘@source, @ref, @version, @annotation’ information to all elements. This change affects: 

pbcoreDescription </br>
pbcoreAssetDate </br>
creator </br>
contributor </br>
publisher </br>
instantiationLocation </br>
instantiationDimensions </br>
instantiationDataRate </br>
instantiationFileSize </br>
instantiationTimeStart </br>
instantiationDuration </br>
instantiationDate </br>
instantiationTracks </br>
instantiationChannelConfiguration </br>
instantiationAlternativeModes </br>
essenceTrackType </br>
essenceTrackDataRate </br>
essenceTrackFrameRate </br>
essenceTrackPlaybackSpeed </br>
essenceTrackSamplingRate </br>
essenceTrackBitDepth </br>
essenceTrackTimeStart </br>
essenceTrackDuration </br>

In all of these cases, these attributes are optional, but they will allow users to document their metadata in greater detail if they so choose. The increased ability to provide URIs for PBCore XML data elements will benefit users who wish to convert their PB Core XML records to Linked Data. Discussions are ongoing with EBU Core to provide a common RDF ontology for this purpose.

Several PBCore elements include attributes -- specifically, the @titleType attribute (for pbcoreTitle), the @subjectType attribute (for pbcoreSubject), and the @affiliation attribute (for pbcoreCreator, pbcoreContributor, and pbcorePublisher) -- for which users also requested the ability to provide the source of the value used to express the type. In future releases of PBCore, the schema could be altered such that these attributes become elements in their own right. However, in order to comply with goal of keeping PBCore 2.1 backwards compatible, this was not possible for 2.1. Therefore, we created several new optional attribute groups for inclusion with the following elements:

**for pbcoreTitle:** </br>
@titleTypeSource </br>
@titleTypeRef </br>
@titleTypeVersion </br>
@titleTypeAnnotation </br>

**for pbcoreSubject:** </br>
@subjectTypeSource </br>
@subjectTypeRef </br>
@subjectTypeVersion </br>
@subjectTypeAnnotation </br>

**for pbcorePart:** </br>
@partType </br>
@partTypeSource </br>
@partTypeRef </br>
@partTypeVersion </br>
@partTypeAnnotation </br>

**for creator, contributor and publisher:** </br>
@affiliationSource </br>
@affiliationRef </br>
@affiliationVersion </br>
@affiliationAnnotation </br>

In PBCore 2.0, the element essenceTrackBitDepth did not include the option to add a @unitofMeasure attribute. PBcore 2.1 now includes this optional attribute.

In PBCore 2.0, the elements instantiationLanguage and essenceTrackLanguage are not repeatable.  This required that if an instantiation or essence track contains multiple languages, both of them would have to be entered in the same data field as three-letter language codes separated by a semicolon, e.g.
	
	<instantiationLanguage>eng;fre</instantiationLanguage>.  
	
While this form of entering data is still valid, we have made those fields repeatable in 2.1 to allow for the option of entering language information separately, e.g. 

	<instantiationLanguage>eng</instantiationLanguage>
	<instantiationLanguage>fre</instantiationLanguage>
	
This allows for more specificity and searchability in entering metadata.  

In order to provide more flexibility in accommodating local metadata elements and values (e.g. from an in-house database), the requirement to use extensionAuthorityUsed when using the container extensionWrap has been removed. However, we still highly recommend using this element whenever possible to document the source system or schema of the element.

One newly suggested element, to define asset version, was approved by the Schema Team.  However, it was not explicitly added to the schema at this time due to the ongoing work to merge some efforts between PBCore and EBUCore (currently limited to a common RDF ontology).  This element does exist in EBUCore; therefore, the team suggests that this (and other similar elements) be considered for future releases of PBCore and/or a future merger with EBUCore. In the meantime, it should be expressed in PBCore using extensions, with the EBUCore element as the extensionElement and EBUCore as extensionAuthorityUsed, as follows:

version - The purpose of this element is to express the version of the intellectual content of the asset being described. In this case, version is specific to content, not to the instantiations of that content (e.g. UK edit, Hulu version, etc.). Use the EBUCore element version to express this information. In a PBCore extension, this could look like:
		
		<extensionWrap>
			<extensionElement>version</extensionElement>
			<extensionValue>Hulu Version</extensionValue>
			<extensionAuthorityUsed>EBUCore</extensionAuthorityUsed>
		</extensionWrap>

The schema team found that several of the issues raised on GitHub were caused by confusion over the definition or usage of an element or attribute. Many of these were addressed by changes to the documentation, specifically the element and attribute definitions, which have been completely revised.  Best practice guidelines for nearly all elements have also been added, and will appear on the website alongside definitions. Longer explanations addressing common use cases (e.g. when and how to use extensions) will be provided in blog posts on the updated PBCore website. 

Several other changes were suggested over the course of this process. Many would require changes that may be implemented for the eventual release of PBCore 3.0, which will provide a broader revision of the PBCore data model. Please also note that this release does not include changes to the PBCore vocabularies. Suggested changes for these are forthcoming.

We welcome your questions and comments about PBCore 2.1!
